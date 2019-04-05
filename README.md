# 创建自定义布局的AlertDialog
## 创建自定义对话框 请创建一个布局，调用 AlertDialog.Builder 对象上的 setView() 将布局添加到 AlertDialog。

![仿真机截图](https://img-blog.csdnimg.cn/20190405231639815.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JlbHRv,size_16,color_FFFFFF,t_70)

activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textid"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="用于测试的内容!"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:clickable="true"/>


</android.support.constraint.ConstraintLayout>
```

MainActivity.java
```
package com.example.cy5962.xmlmenu_demo;

import android.content.DialogInterface;
import android.graphics.Color;
import android.support.v7.app.AlertDialog;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.Menu;
import android.view.MenuInflater;
import android.view.MenuItem;
import android.widget.TextView;
import android.widget.Toast;
public class MainActivity extends AppCompatActivity {

    private final int size=110;
    private final int common=111;
    private final int color=112;
    private TextView textId;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        textId=(TextView)findViewById(R.id.textid);
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        menu.add(1,size,1,"字体大小");
        menu.add(1,common,2,"普通菜单项");
        menu.add(1,color,3,"字体颜色");
        return super.onCreateOptionsMenu(menu);
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        int id=item.getItemId();
        switch (id){
            case size:
                final AlertDialog.Builder builder=new AlertDialog.Builder(this);
                builder.setTitle("设置字体大小");
                builder.setSingleChoiceItems(new String[]{"10号字体","16号字体","20号字体"},-1,new DialogInterface.OnClickListener(){
                    @Override
                    public void onClick(DialogInterface dialogInterface, int i) {
                        switch (i){
                            case 0:textId.setTextSize(10);
                                dialogInterface.dismiss();
                                break;
                            case 1:textId.setTextSize(16);
                                dialogInterface.dismiss();
                                break;
                            case 2:textId.setTextSize(20);
                                dialogInterface.dismiss();
                                break;
                        }
                    }
                });
                builder.setNegativeButton("取消",null);
                builder.show();
                break;
            case common:
                Toast.makeText(this,"你点击了普通菜单项", Toast.LENGTH_LONG).show();
                break;
            case color:
                final AlertDialog.Builder builder2=new AlertDialog.Builder(this);
                builder2.setTitle("设置字体颜色");
                builder2.setSingleChoiceItems(new String[]{"红色","黑色","蓝色"},-1,new DialogInterface.OnClickListener(){
                    @Override
                    public void onClick(DialogInterface dialogInterface, int i) {
                        switch (i){
                            case 0:textId.setTextColor(Color.RED);
                                dialogInterface.dismiss();
                                break;
                            case 1:textId.setTextColor(Color.BLACK);
                                dialogInterface.dismiss();
                                break;
                            case 2:textId.setTextColor(Color.BLUE);
                                dialogInterface.dismiss();
                                break;
                        }
                    }
                });
                builder2.setNegativeButton("取消",null);
                builder2.show();
                break;
        }
        return super.onOptionsItemSelected(item);
    }
}
```

