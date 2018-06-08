# NotePad
This is an AndroidStudio rebuild of google SDK sample NotePad
## 时间
![image](https://github.com/vonus123/NotePad-master/blob/master/Screenshot_1528300020.png)
### NoteList中显示条目增加时间戳显示
    	Long now = Long.valueOf(System.currentTimeMillis());
        Date date = new Date(System.currentTimeMillis());
        SimpleDateFormat format = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String dateTime = format.format(date);
	<TextView
		android:id="@+id/text1_time"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:textAppearance="?android:attr/textAppearanceSmall"
		android:paddingLeft="5dip"
		android:textColor="#01010e"/>
	
## search
### 添加笔记查询功能（根据标题查询）
![image](https://github.com/vonus123/NotePad-master/blob/master/Screenshot_1528300099.png)
	
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.note_search_list);
		Intent intent = getIntent();
		if (intent.getData() == null) {
		    intent.setData(NotePad.Notes.CONTENT_URI);
		}
		SearchView searchview = (SearchView)findViewById(R.id.search_view);
		searchview.setOnQueryTextListener(NoteSearch.this);  //为查询文本框注册监听器
	    }
	   <SearchView
		android:id="@+id/search_view"
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:iconifiedByDefault="false"
		android:queryHint="输入搜索内容..."
		android:layout_alignParentTop="true">
	    </SearchView>

    <ListView
        android:id="@android:id/list"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
    </ListView>

## UI美化
![image](https://github.com/vonus123/NotePad-master/blob/master/Screenshot_1528299366.png)

 	public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.note_color);
        mUri = getIntent().getData();
        mCursor = managedQuery(
                mUri,        // The URI for the note that is to be retrieved.
                PROJECTION,  // The columns to retrieve
                null,        // No selection criteria are used, so no where columns are needed.
                null,        // No where columns are used, so no where values are needed.
                null         // No sort order is needed.
        );

    }
 ### 跳转改变颜色的activity，将uri信息传到新的activity
    private final void changeColor() {
        Intent intent = new Intent(null,mUri);
        intent.setClass(NoteEditor.this,NoteColor.class);
        NoteEditor.this.startActivity(intent);
    }
     private static final String[] PROJECTION = new String[] {
            NotePad.Notes._ID, // 0
            NotePad.Notes.COLUMN_NAME_TITLE, // 1
            NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE, // 2
            NotePad.Notes.COLUMN_NAME_BACK_COLOR,
	}; 
	case R.id.menu_bcolor:
                changeColor();
                break;
### 使用线性布局
	 <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:orientation="horizontal"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    android:paddingLeft="28dp">

    <ImageButton
        android:id="@+id/color_white"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:background="@color/colorWhite"
        android:onClick="white"/>
    <ImageButton
        android:id="@+id/color_yellow"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:background="@color/colorYellow"
        android:onClick="yellow"/>
    <ImageButton
        android:id="@+id/color_blue"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:background="@color/colorBlue"
        android:onClick="blue"/>
    <ImageButton
        android:id="@+id/color_green"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:background="@color/colorGreen"
        android:onClick="green"/>
    <ImageButton
        android:id="@+id/color_red"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:background="@color/colorRed"
        android:onClick="red"/>
</LinearLayout>
###  复制粘贴paste

![image](https://github.com/vonus123/NotePad-master/blob/master/Screenshot_1528299461.png)
###   删除delete

	 case R.id.menu_delete:
			deleteNote();
			finish();
			break;
###   按时间排序（创建时间或者修改时间）

![image](https://github.com/vonus123/NotePad-master/blob/master/Screenshot_1528299375.png)

