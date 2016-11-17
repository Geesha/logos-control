<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="complanydomain.logoscontrol.MainActivity"
    android:focusable="true"
    android:focusableInTouchMode="true">

    <EditText
        android:id="@+id/desiredIp"
        android:layout_width="200dp"
        android:layout_height="wrap_content"
        android:inputType="phone"
        android:digits="0123456789."
        android:maxLength="15"
        android:ems="14"
        android:imeOptions="flagNoFullscreen"
        android:background="@android:drawable/editbox_background"
        android:textCursorDrawable="@null"
        android:hint="IP Address"/>
    <EditText
        android:id="@+id/desiredName"
        android:layout_width="200dp"
        android:layout_height="wrap_content"
        android:inputType="text"
        android:maxLength="20"
        android:ems="14"
        android:layout_marginTop="40dp"
        android:imeOptions="flagNoFullscreen"
        android:background="@android:drawable/editbox_background"
        android:textCursorDrawable="@null"
        android:hint="Name"/>

    <TextView
        android:text="Relay 3"
        android:layout_width="50dp"
        android:layout_height="20dp"
        android:layout_below="@id/desiredName"
        android:layout_centerHorizontal="true"
        android:layout_marginLeft="8.5dp"
        android:layout_marginRight="10dp"
        android:id="@+id/relay_3_text"/>
    <TextView
        android:text="Relay 2"
        android:layout_width="50dp"
        android:layout_height="20dp"
        android:layout_below="@id/desiredName"
        android:layout_toLeftOf="@id/relay_3_text"
        android:layout_marginLeft="7dp"
        android:layout_marginRight="7dp"
        android:id="@+id/relay_2_text"/>
    <TextView
        android:text="Relay 1"
        android:layout_width="50dp"
        android:layout_height="20dp"
        android:layout_below="@id/desiredName"
        android:layout_toLeftOf="@id/relay_2_text"
        android:layout_marginLeft="7dp"
        android:layout_marginRight="7dp"
        android:id="@+id/relay_1_text"/>
    <TextView
        android:text="Relay 4"
        android:layout_width="50dp"
        android:layout_height="20dp"
        android:layout_below="@id/desiredName"
        android:layout_toRightOf="@id/relay_3_text"
        android:layout_marginLeft="7dp"
        android:layout_marginRight="7dp"
        android:id="@+id/relay_4_text"/>
    <TextView
        android:text="Relay 5"
        android:layout_width="50dp"
        android:layout_height="20dp"
        android:layout_below="@id/desiredName"
        android:layout_toRightOf="@id/relay_4_text"
        android:layout_marginLeft="7dp"
        android:layout_marginRight="7dp"
        android:id="@+id/relay_5_text"/>

    <Switch
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/relay_3_text"
        android:layout_centerHorizontal="true"
        android:switchMinWidth="50dp"
        android:textOff=""
        android:textOn=""
        android:layout_marginLeft="7dp"
        android:layout_marginRight="7dp"
        android:id="@+id/relay_3"
        />
    <Switch
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/relay_2_text"
        android:layout_toLeftOf="@id/relay_3"
        android:switchMinWidth="50dp"
        android:textOff=""
        android:textOn=""
        android:layout_marginLeft="7dp"
        android:layout_marginRight="7dp"
        android:id="@+id/relay_2"
        />
    <Switch
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/relay_1_text"
        android:layout_toLeftOf="@id/relay_2"
        android:switchMinWidth="50dp"
        android:textOff=""
        android:textOn=""
        android:layout_marginLeft="7dp"
        android:layout_marginRight="7dp"
        android:id="@+id/relay_1"
        />
    <Switch
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/relay_4_text"
        android:layout_toRightOf="@id/relay_3"
        android:switchMinWidth="50dp"
        android:textOff=""
        android:textOn=""
        android:layout_marginLeft="7dp"
        android:layout_marginRight="7dp"
        android:id="@+id/relay_4" />
    <Switch
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/relay_5_text"
        android:layout_toRightOf="@id/relay_4"
        android:switchMinWidth="50dp"
        android:textOff=""
        android:textOn=""
        android:layout_marginLeft="7dp"
        android:layout_marginRight="7dp"
        android:id="@+id/relay_5"
        />
    <Button
        android:layout_width="90dp"
        android:layout_height="wrap_content"
        android:layout_toRightOf="@id/desiredIp"
        android:id="@+id/checkRelays"
        android:layout_marginTop="13dp"
        android:text="Connect"/>

    <TextView
        android:layout_width="match_parent"
        android:layout_height="20dp"
        android:layout_below="@id/relay_1"
        android:id="@+id/response"
        android:textColor="#fa0000"
        android:text="Disconnected"/>



    <TextView
        android:id="@+id/recents"
        android:text="▼Recents▼"
        android:textColor="#2222ff"
        android:textSize="13sp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/response"/>

    <ListView
        android:id="@+id/listRecent"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/recents"/>



</RelativeLayout>
