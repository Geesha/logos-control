package complanydomain.logoscontrol;

import android.app.ProgressDialog;
import android.content.Context;
import android.content.SharedPreferences;
import android.graphics.Color;
import android.graphics.PorterDuff;
import android.os.AsyncTask;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Base64;
import android.view.ContextMenu;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.view.inputmethod.InputMethodManager;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.CompoundButton;
import android.widget.EditText;
import android.widget.ListView;
import android.widget.Switch;
import android.widget.TextView;
import android.widget.Toast;
import android.widget.ToggleButton;

import java.io.BufferedInputStream;
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;
import java.security.Key;
import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.Set;
import java.util.Timer;
import java.util.TimerTask;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

import static android.R.drawable.editbox_background;
import static android.R.drawable.editbox_background_normal;

public class MainActivity extends AppCompatActivity {

    Switch relay_1;
    Switch relay_2;
    Switch relay_3;
    Switch relay_4;
    Switch relay_5;
    TextView relay_1_text;
    TextView relay_2_text;
    TextView relay_3_text;
    TextView relay_4_text;
    TextView relay_5_text;
    Button checkRelays;
    TextView responseText;
    String ip = "0.0.0.0";
    String name;
    String action;
    String relayId;
    String relayState;
    EditText desiredIp;
    EditText desiredName;
    ArrayAdapter<String> adapter;
    List<String> listOfAdresses = new ArrayList<>();
    ListView recentlyUsed;
    String[] menuItems = new String[]{"Delete"};


    SharedPreferences sharedpreferences;

    private final String ADDRESSES = "recent_addresses";
    public String[] arrayHeaders = new String[0];

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


        sharedpreferences = getSharedPreferences(getPackageName(), Context.MODE_PRIVATE);
        final Set<String> set = sharedpreferences.getStringSet(ADDRESSES, new HashSet<String>());
        listOfAdresses = new ArrayList<String>(set);

        recentlyUsed = (ListView) findViewById(R.id.listRecent);

        adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, listOfAdresses);

        recentlyUsed.setAdapter(adapter);
        registerForContextMenu(recentlyUsed);

        relay_1 = (Switch) findViewById(R.id.relay_1);
        relay_2 = (Switch) findViewById(R.id.relay_2);
        relay_3 = (Switch) findViewById(R.id.relay_3);
        relay_4 = (Switch) findViewById(R.id.relay_4);
        relay_5 = (Switch) findViewById(R.id.relay_5);
        relay_1_text = (TextView) findViewById(R.id.relay_1_text);
        relay_2_text = (TextView) findViewById(R.id.relay_2_text);
        relay_3_text = (TextView) findViewById(R.id.relay_3_text);
        relay_4_text = (TextView) findViewById(R.id.relay_4_text);
        relay_5_text = (TextView) findViewById(R.id.relay_5_text);
        checkRelays = (Button) findViewById(R.id.checkRelays);
        responseText = (TextView) findViewById(R.id.response);
        desiredIp = (EditText) findViewById(R.id.desiredIp);
        desiredName = (EditText) findViewById(R.id.desiredName);

        relay_1.setVisibility(View.GONE);
        relay_2.setVisibility(View.GONE);
        relay_3.setVisibility(View.GONE);
        relay_4.setVisibility(View.GONE);
        relay_5.setVisibility(View.GONE);
        relay_1_text.setVisibility(View.GONE);
        relay_2_text.setVisibility(View.GONE);
        relay_3_text.setVisibility(View.GONE);
        relay_4_text.setVisibility(View.GONE);
        relay_5_text.setVisibility(View.GONE);

        final SharedPreferences.Editor editor = sharedpreferences.edit();


        relay_1.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {

                //ip = desiredIp.getText().toString();

                if (isChecked) {
                    action = "relays/11";
                } else {
                    action = "relays/10";
                }

                new GetClass(MainActivity.this).execute();

                InputMethodManager imm = (InputMethodManager) getSystemService(INPUT_METHOD_SERVICE);
                imm.hideSoftInputFromWindow(getCurrentFocus().getWindowToken(), 0);
                //Toast.makeText(MainActivity.this,
                //        "Triggering relay 1 ", Toast.LENGTH_SHORT).show();

            }
        });

        relay_2.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {

                //ip = desiredIp.getText().toString();

                if (isChecked) {
                    action = "relays/21";
                } else {
                    action = "relays/20";
                }

                new GetClass(MainActivity.this).execute();


                InputMethodManager imm = (InputMethodManager) getSystemService(INPUT_METHOD_SERVICE);
                imm.hideSoftInputFromWindow(getCurrentFocus().getWindowToken(), 0);
                //Toast.makeText(MainActivity.this,
                //        "Triggering relay 2", Toast.LENGTH_SHORT).show();
            }
        });

        relay_3.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {

                //ip = desiredIp.getText().toString();

                if (isChecked) {
                    action = "relays/31";
                } else {
                    action = "relays/30";
                }

                new GetClass(MainActivity.this).execute();

                InputMethodManager imm = (InputMethodManager) getSystemService(INPUT_METHOD_SERVICE);
                imm.hideSoftInputFromWindow(getCurrentFocus().getWindowToken(), 0);
                //Toast.makeText(MainActivity.this,
                //        "Triggering relay 3", Toast.LENGTH_SHORT).show();
            }
        });

        relay_4.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {

                //ip = desiredIp.getText().toString();

                if (isChecked) {
                    action = "relays/41";
                } else {
                    action = "relays/40";
                }

                new GetClass(MainActivity.this).execute();

                InputMethodManager imm = (InputMethodManager) getSystemService(INPUT_METHOD_SERVICE);
                imm.hideSoftInputFromWindow(getCurrentFocus().getWindowToken(), 0);
                //Toast.makeText(MainActivity.this,
                //        "Triggering relay 4", Toast.LENGTH_SHORT).show();
            }
        });

        relay_5.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {

                //ip = desiredIp.getText().toString();

                if (isChecked) {
                    action = "relays/51";
                } else {
                    action = "relays/50";
                }

                new GetClass(MainActivity.this).execute();

                InputMethodManager imm = (InputMethodManager) getSystemService(INPUT_METHOD_SERVICE);
                imm.hideSoftInputFromWindow(getCurrentFocus().getWindowToken(), 0);
                //Toast.makeText(MainActivity.this,
                //        "Triggering relay 5", Toast.LENGTH_SHORT).show();
            }
        });

        checkRelays.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {

                ip = vaidIp(desiredIp.getText().toString());
                name = desiredName.getText().toString();
                action = "relays/99";

                if (ip.equals("0.0.0.0")){
                    Toast.makeText(MainActivity.this,
                            "Wrong IP !", Toast.LENGTH_SHORT).show();
                } else {



                    InputMethodManager imm = (InputMethodManager) getSystemService(INPUT_METHOD_SERVICE);
                    imm.hideSoftInputFromWindow(getCurrentFocus().getWindowToken(), 0);

                    new GetClass(MainActivity.this).execute();

                    Toast.makeText(MainActivity.this,
                            "Getting relays state...", Toast.LENGTH_SHORT).show();

                    if (!listOfAdresses.contains("Name: " + name + "     IP: " + ip)) {
                        listOfAdresses.add(0, "Name: " + name + "     IP: " + ip);
                    }

                    adapter.notifyDataSetChanged();
                    Set<String> set = new HashSet<String>();
                    set.addAll(listOfAdresses);
                    editor.putStringSet(ADDRESSES, set);
                    editor.apply();
                }
            }
        });

        desiredIp.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                desiredIp.setBackgroundResource(editbox_background);
                desiredIp.setCursorVisible(true);
            }
        });
        desiredName.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                desiredName.setBackgroundResource(editbox_background);
                desiredName.setCursorVisible(true);
            }
        });


        recentlyUsed.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            public void onItemClick(AdapterView<?> adapterView, View view, int position, long id) {


                desiredIp.setText(listOfAdresses.get(position).substring(listOfAdresses.get(position).indexOf("IP: ") + 4
                        , listOfAdresses.get(position).length()));
                desiredName.setText(listOfAdresses.get(position).substring(listOfAdresses.get(position).indexOf("Name: ") + 6
                        , listOfAdresses.get(position).indexOf("     IP: ")));

                InputMethodManager imm = (InputMethodManager) getSystemService(INPUT_METHOD_SERVICE);
                imm.hideSoftInputFromWindow(getCurrentFocus().getWindowToken(), 0);

            }
        });

    }

    private class GetClass extends AsyncTask<String, Void, String> {

        private ProgressDialog progress;

        private final Context context;

        public GetClass(Context c){
            this.context = c;
        }

        protected void onPreExecute(){
            progress = new ProgressDialog(this.context);
            progress.setMessage("Loading");
            progress.show();
            relay_1.setClickable(false);
            relay_2.setClickable(false);
            relay_3.setClickable(false);
            relay_4.setClickable(false);
            relay_5.setClickable(false);
        }

        @Override
        protected String doInBackground(String... params) {

                        

            String apiKey = "6da13b696f737097e0146e47cc0d0985";
            String result = "";

                try {

                    URL url = new URL("http://" + ip + "/tp/v1/" + action);

                    HttpURLConnection connection = (HttpURLConnection) url.openConnection();

                    connection.setRequestMethod("GET");
                    connection.addRequestProperty("authorization", apiKey);

                    connection.setUseCaches(false);
                    connection.setDoInput(true);
                    connection.setDoOutput(false);
                    connection.connect();
                    connection.setInstanceFollowRedirects(true);

                    int responseCode = connection.getResponseCode();

                    InputStream in = null;
                    int status = connection.getResponseCode();

                    if (status >= HttpURLConnection.HTTP_BAD_REQUEST)
                        in = connection.getErrorStream();
                    else
                        in = connection.getInputStream();

                    BufferedReader br = new BufferedReader(new InputStreamReader(in));
                    String line = "";
                    StringBuilder responseOutput = new StringBuilder();
                    while ((line = br.readLine()) != null) {
                        responseOutput.append(line);
                    }
                    br.close();

                        result = responseOutput.toString();
                        relayState = "" + responseCode;

                } catch (MalformedURLException e) {
                    // TODO Auto-generated catch block
                    e.printStackTrace();
                } catch (IOException e) {
                    // TODO Auto-generated catch block
                    e.printStackTrace();
                }

                return result;
            }

        protected void onPostExecute(String result) {

            //if (relayState.contains("200")){
            //    Toast.makeText(MainActivity.this,
            //            "Successful !", Toast.LENGTH_SHORT).show();
            //} else {
            //    Toast.makeText(MainActivity.this,
            //            "Error while connecting, please check IP !", Toast.LENGTH_LONG).show();
            //}

            if (result.contains("false")) {

                //Toast.makeText(MainActivity.this,
                //        "Successful !", Toast.LENGTH_SHORT).show();

                responseText.setText("Connected to " + ip);

                if (result.contains("11")) {
                    relay_1.setChecked(true);
                }
                if (result.contains("21")) {
                    relay_2.setChecked(true);
                }
                if (result.contains("31")) {
                    relay_3.setChecked(true);
                }
                if (result.contains("41")) {
                    relay_4.setChecked(true);
                }
                if (result.contains("51")) {
                    relay_5.setChecked(true);
                }
                if (result.contains("10")) {
                    relay_1.setChecked(false);
                }
                if (result.contains("20")) {
                    relay_2.setChecked(false);
                }
                if (result.contains("30")) {
                    relay_3.setChecked(false);
                }
                if (result.contains("40")) {
                    relay_4.setChecked(false);
                }
                if (result.contains("50")) {
                    relay_5.setChecked(false);
                }

                relay_1_text.setVisibility(View.VISIBLE);
                relay_2_text.setVisibility(View.VISIBLE);
                relay_3_text.setVisibility(View.VISIBLE);
                relay_4_text.setVisibility(View.VISIBLE);
                relay_5_text.setVisibility(View.VISIBLE);
                relay_1.setVisibility(View.VISIBLE);
                relay_2.setVisibility(View.VISIBLE);
                relay_3.setVisibility(View.VISIBLE);
                relay_4.setVisibility(View.VISIBLE);
                relay_5.setVisibility(View.VISIBLE);
                relay_1.setClickable(true);
                relay_2.setClickable(true);
                relay_3.setClickable(true);
                relay_4.setClickable(true);
                relay_5.setClickable(true);
            } else {
                Toast.makeText(MainActivity.this,
                        "Error! Check IP/Internet Connection", Toast.LENGTH_LONG).show();
                responseText.setText("Disconnected");
                relay_1.setClickable(false);
                relay_2.setClickable(false);
                relay_3.setClickable(false);
                relay_4.setClickable(false);
                relay_5.setClickable(false);
            }

            progress.dismiss();
        }

    }
    public void onCreateContextMenu(ContextMenu menu, View v,
                                    ContextMenu.ContextMenuInfo menuInfo) {
        arrayHeaders = listOfAdresses.toArray(new String[0]);
        if (v.getId() == R.id.listRecent) {
            AdapterView.AdapterContextMenuInfo info = (AdapterView.AdapterContextMenuInfo) menuInfo;
            menu.setHeaderTitle(arrayHeaders[info.position]);
            for (int i = 0; i < menuItems.length; i++) {
                menu.add(Menu.NONE, i, i, menuItems[i]);
            }
        }
    }
    public boolean onContextItemSelected(MenuItem item) {
        AdapterView.AdapterContextMenuInfo info = (AdapterView.AdapterContextMenuInfo) item.getMenuInfo();

        final SharedPreferences.Editor editor = sharedpreferences.edit();

        int menuItemIndex = item.getItemId();
        String menuItemName = menuItems[menuItemIndex];
        String listItemName = arrayHeaders[info.position];

        listOfAdresses.remove(listItemName);
        adapter.notifyDataSetChanged();
        Set<String> set = new HashSet<String>();
        set.addAll(listOfAdresses);
        editor.putStringSet(ADDRESSES, set);
        editor.apply();


        Toast.makeText(MainActivity.this,
                "Address ' " + listItemName + " ' deleted !", Toast.LENGTH_SHORT).show();

        return true;
    }

    private String vaidIp(String ipString) {
        String IPADDRESS_PATTERN =
                "(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)";

        Pattern pattern = Pattern.compile(IPADDRESS_PATTERN);
        Matcher matcher = pattern.matcher(ipString);
        if (matcher.find()) {
            return matcher.group();
        }
        else{
            return "0.0.0.0";
        }
    }
}
