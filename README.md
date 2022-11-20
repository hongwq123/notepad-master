# NotePad  

1.添加时间戳  
(1)修改NotesList.java中PROJECTION，添加modif字段  
NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE  
(2)增加dataColumns中装配到ListView的内容  
NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE}  
(3)增加一个textview组件放时间  
<TextView  
        android:id="@+id/text2"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:textAppearance="?android:attr/textAppearanceLarge"  
        android:gravity="center_vertical"  
        android:singleLine="true"/>  
(4)修改NoteEditor.java中updateNote方法中的时间类型  
 SimpleDateFormat sf = new SimpleDateFormat("yy/MM/dd HH:mm");  
        Date d = new Date(now);  
        String format = sf.format(d);  
![时间戳实现](https://github.com/hongwq123/notepad-master/blob/main/jietu1/3.png—)  
2.添加查询功能  
(1)在AndroidManifest.xml里注册NoteSearch  
<activity android:name=".NoteSearch" android:label="@string/search_note" />  
(2)在list_options_menu.xml布局文件中添加搜索功能  
    <item  
        android:id="@+id/menu_search"  
        android:icon="@android:drawable/ic_menu_search"  
        android:title="@string/menu_search"  
        android:showAsAction="always" />  
(3)新建布局文件note_search
<?xml version="1.0" encoding="utf-8"?>  
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"  
    android:layout_width="match_parent"  
    android:layout_height="match_parent"  
    android:orientation="vertical">  
    <SearchView
        android:id="@+id/search_view"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        android:iconifiedByDefault="false"  
        />  
    <ListView  
        android:id="@+id/list_view"  
        android:layout_width="match_parent"  
        android:layout_height="wrap_content"  
        />  
</LinearLayout>  
(4)添加search查询的处理  
        case R.id.menu_search:  
          Intent intent = new Intent(this, NoteSearch.class);  
          this.startActivity(intent);  
          return true;  
(5)编写一个查询的java代码notesearch,实现查询功能  
![查询功能实现](https://github.com/hongwq123/notepad-master/blob/main/jietu1/2.png—)  
3.界面UI美化  
(1)将主题换为白色  
        <activity android:name="NotesList" android:label="@string/title_notes_list"  
                  android:theme="@android:style/Theme.Holo.Light">  
(2)添加
        public static final String COLUMN_NAME_BACK_COLOR = "color";  
(3)添加颜色的字段  
+ NotePad.Notes.COLUMN_NAME_BACK_COLOR + " INTEGER"   
(4)定义颜色  
        public static final int DEFAULT_COLOR = 0; //white  
        public static final int YELLOW_COLOR = 1; //yellow  
        public static final int BLUE_COLOR = 2; //blue  
        public static final int GREEN_COLOR = 3; //green  
        public static final int RED_COLOR = 4; //red  （
(5)自定义一个MyCursorAdapter.java继承SimpleCursorAdapter  
(6)在PROJECTION添加颜色项  
    private static final String[] PROJECTION = new String[] {  
            NotePad.Notes._ID, // 0  
            NotePad.Notes.COLUMN_NAME_TITLE, // 1  
            //Extended:display time, color  
            NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE, // 2  
            NotePad.Notes.COLUMN_NAME_BACK_COLOR  
    };  
(7)SimpleCursorAdapter改为使用MyCursorAdapte
        MyCursorAdapter adapter = new MyCursorAdapter(  
                this,  
                R.layout.noteslist_item,  
                cursor,  
                dataColumns,  
                viewIDs  
        );  
![时间戳实现](https://github.com/hongwq123/notepad-master/blob/main/jietu1/1.png—)  
