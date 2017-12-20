Data
import java.util.ArrayList;

/**
 * Created by admin on 12/6/2017.
 */

public class Data {

    static String main="";
static  ArrayList<String> strings;

     ArrayList<String> getg(){
         ArrayList<String> strings=new ArrayList();
         strings.add("POP ROCK");
         strings.add("POP");
         strings.add("ELECTRONIC");
         strings.add("JAZZ");
         strings.add("ROCK");
         strings.add("CLASSICAL");
         strings.add("LOUNGE");
         strings.add("FASHION");
         strings.add("EVENING");
         strings.add("PIANO");
         strings.add("ACOUSTIC");
         strings.add("ROMANCE");
         strings.add("AMBIENT");
         strings.add("DANCE");
         strings.add("FRENCH");
         strings.add("WORLD");
         strings.add("ENERGY");
         strings.add("SUNNY");
         strings.add("CHRITMAS");
         strings.add("INDIE");

         strings.add("BEST OF");
         strings.add("COOL");
         strings.add("SMOOTH");
         strings.add("LATIN");
         strings.add("CASUAL");
         strings.add("CAFE");
         strings.add("FITNESS");
         strings.add("FOLK");
         strings.add("ITALIAN");
         strings.add("URBAN");
         strings.add("COUNTRY");
         strings.add("DEEP VIBES");
         return strings;


     }
    ArrayList<String> getop(){
        ArrayList<String> strings=new ArrayList();
        strings.add("SAD");
        strings.add("LOVE");
        strings.add("HAPPY");
        strings.add("EMOTIONAL");
        strings.add("HIPHOP");
        strings.add("SOUNDTRACK");
        strings.add("DANCE");
        strings.add("DARK");
        strings.add("CHILLOUT");
        strings.add("COVER");
        strings.add("RNB");
        strings.add("METAL");
        strings.add("SOFT");
        strings.add("DREAM");
        strings.add("NEO");
        strings.add("UNDERGROUND");
        strings.add("RELAX");
        strings.add("PUNK");
        strings.add("JAZZY");
        strings.add("KIDS");
        return strings;


    }

    ArrayList<String> gett(){
        ArrayList<String> strings=new ArrayList();
        strings.add("MAN");
        strings.add("WOMAN");
        strings.add("DJ");
        strings.add("TRUE");
        strings.add("REMIX");
        strings.add("POWER");
        strings.add("INDIAN");
        strings.add("SCHOOL");
        strings.add("BEST");
        strings.add("TOP");
        strings.add("TRACK");
        strings.add("BRAZILIAN");
        strings.add("SAMBA");
        strings.add("COCKTAIL");
        strings.add("MIX");
        strings.add("REMIX");
        strings.add("BASS");
        strings.add("BOOST");
        strings.add("HIGH");
        strings.add("BOOSTED");
        return strings;


    }



}
------------------------------------------------------------------------------------------------
DataParserObject
import android.support.annotation.NonNull;
import android.util.Log;

import com.squareup.okhttp.OkHttpClient;
import com.squareup.okhttp.Request;
import com.squareup.okhttp.Response;

import org.json.JSONException;
import org.json.JSONObject;

import java.io.IOException;


public class DataParserObject {
private static final String api = "https://api.jamendo.com/v3.0/tracks/?client_id=2aa01bca&format=jsonpretty&limit=200&namesearch=";
    public static final String TAG = "api_data";


    private static Response returndata;

    public static JSONObject getDataFromWeb(String s) {
        try {
            OkHttpClient okHttpClient = new OkHttpClient();
            Request build = new Request.Builder()
                    .url(api +s)
                    .build();
            returndata = okHttpClient.newCall(build).execute();
            return new JSONObject(returndata.body().string());
        } catch (@NonNull IOException | JSONException e) {
            Log.e(TAG, "" + e.getLocalizedMessage());
        }
        return null;
    }
}
---------------------------------------------------------------------------------------------------------------
MainActivity
import android.Manifest;
import android.content.Intent;
import android.content.pm.PackageManager;
import android.os.Bundle;
import android.support.design.widget.FloatingActionButton;
import android.support.design.widget.Snackbar;
import android.support.v4.app.ActivityCompat;
import android.support.v4.content.ContextCompat;
import android.view.View;
import android.support.design.widget.NavigationView;
import android.support.v4.view.GravityCompat;
import android.support.v4.widget.DrawerLayout;
import android.support.v7.app.ActionBarDrawerToggle;
import android.support.v7.app.AppCompatActivity;
import android.support.v7.widget.Toolbar;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.EditText;
import android.widget.RelativeLayout;
import android.widget.TextView;

import com.google.android.gms.ads.AdListener;
import com.google.android.gms.ads.AdRequest;
import com.google.android.gms.ads.InterstitialAd;
import com.google.android.gms.ads.MobileAds;

public class MainActivity extends AppCompatActivity
        implements NavigationView.OnNavigationItemSelectedListener {

    RelativeLayout img1,img2,img3,img4,img5,img6,img7,img8,img9,img10,img11,img12,img13,img14,img15,img16,img17,img18,gener,trending,top;
EditText  editText;
    TextView textView;
    private InterstitialAd mInterstitialAd;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        MobileAds.initialize(this, "YOUR_ADMOB_APP_ID");
        mInterstitialAd = new InterstitialAd(this);
        mInterstitialAd.setAdUnitId("ca-app-pub-3940256099942544/1033173712");
        mInterstitialAd.loadAd(new AdRequest.Builder().build());

        mInterstitialAd.setAdListener(new AdListener() {
            @Override
            public void onAdLoaded() {
                // Code to be executed when an ad finishes loading.
            }

            @Override
            public void onAdFailedToLoad(int errorCode) {
                // Code to be executed when an ad request fails.
            }

            @Override
            public void onAdOpened() {
                // Code to be executed when the ad is displayed.
            }

            @Override
            public void onAdLeftApplication() {
                // Code to be executed when the user has left the app.
            }

            @Override
            public void onAdClosed() {
                mInterstitialAd.loadAd(new AdRequest.Builder().build());
                Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                startActivity(intent);
                // Code to be executed when when the interstitial ad is closed.
            }
        });





        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);


        DrawerLayout drawer = (DrawerLayout) findViewById(R.id.drawer_layout);
        ActionBarDrawerToggle toggle = new ActionBarDrawerToggle(
                this, drawer, toolbar, R.string.navigation_drawer_open, R.string.navigation_drawer_close);
        drawer.setDrawerListener(toggle);
        toggle.syncState();

        NavigationView navigationView = (NavigationView) findViewById(R.id.nav_view);
        navigationView.setNavigationItemSelectedListener(this);


        editText=(EditText) findViewById(R.id.editText);
        textView=(TextView) findViewById(R.id.textView2);
        textView.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=editText.getText().toString();

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);



            }
        });
        gener=(RelativeLayout) findViewById(R.id.gener);
        gener.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                Data.strings=new Data().getg();
                Intent intent=new Intent(MainActivity.this,TreActivity.class);
                startActivity(intent);
            }
        });
        trending=(RelativeLayout) findViewById(R.id.trending);
        trending.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                Data.strings=new Data().gett();
                Intent intent=new Intent(MainActivity.this,TreActivity.class);
                startActivity(intent);
            }
        });
        top=(RelativeLayout) findViewById(R.id.top);
        top.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                Data.strings=new Data().getop();
                Intent intent=new Intent(MainActivity.this,TreActivity.class);
                startActivity(intent);
            }
        });
        img1=(RelativeLayout) findViewById(R.id.img1);
        img1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getg().get(0);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }

            }
        });

        img2=(RelativeLayout) findViewById(R.id.img2);
        img2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getg().get(1);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        });
        img3=(RelativeLayout) findViewById(R.id.img3);
        img3.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getg().get(2);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        });
        img4=(RelativeLayout) findViewById(R.id.img4);
        img4.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getg().get(3);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img5=(RelativeLayout) findViewById(R.id.img5);
        img5.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getg().get(4);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img6=(RelativeLayout) findViewById(R.id.img6);
        img6.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getg().get(5);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img7=(RelativeLayout) findViewById(R.id.img7);
        img7.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().gett().get(0);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img8=(RelativeLayout) findViewById(R.id.img8);
        img8.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().gett().get(1);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img9=(RelativeLayout) findViewById(R.id.img9);
        img9.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().gett().get(2);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img10=(RelativeLayout) findViewById(R.id.img10);
        img10.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().gett().get(3);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img11=(RelativeLayout) findViewById(R.id.img11);
        img11.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().gett().get(4);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img12=(RelativeLayout) findViewById(R.id.img12);
        img12.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().gett().get(5);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img13=(RelativeLayout) findViewById(R.id.img13);
        img13.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getop().get(0);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img14=(RelativeLayout) findViewById(R.id.img14);
        img14.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getop().get(1);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img15=(RelativeLayout) findViewById(R.id.img15);
        img15.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getop().get(2);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img16=(RelativeLayout) findViewById(R.id.img16);
        img16.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getop().get(3);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        }); img17=(RelativeLayout) findViewById(R.id.img17);
        img17.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getop().get(4);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        });

        img18=(RelativeLayout) findViewById(R.id.img18);
        img18.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Data.main=new Data().getop().get(5);
                if (mInterstitialAd.isLoaded()) {
                    mInterstitialAd.show();
                } else {

                    Intent intent=new Intent(MainActivity.this,RecycleActivity.class);
                    startActivity(intent);
                }
            }
        });







        if (ContextCompat.checkSelfPermission(MainActivity.this,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)
                != PackageManager.PERMISSION_GRANTED) {

            if (ActivityCompat.shouldShowRequestPermissionRationale(MainActivity.this,
                    Manifest.permission.WRITE_EXTERNAL_STORAGE)) {

                ActivityCompat.requestPermissions(MainActivity.this,
                        new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                        10);

            } else {

                ActivityCompat.requestPermissions(MainActivity.this,
                        new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                        10);

            }
        }





    }

    @Override
    public void onBackPressed() {
        DrawerLayout drawer = (DrawerLayout) findViewById(R.id.drawer_layout);
        if (drawer.isDrawerOpen(GravityCompat.START)) {
            drawer.closeDrawer(GravityCompat.START);
        } else {
            super.onBackPressed();
        }
    }



    @SuppressWarnings("StatementWithEmptyBody")
    @Override
    public boolean onNavigationItemSelected(MenuItem item) {
        // Handle navigation view item clicks here.
        int id = item.getItemId();

        if (id == R.id.gener) {
            Data.strings=new Data().getg();
            Intent intent=new Intent(MainActivity.this,TreActivity.class);
            startActivity(intent);

        } else if (id == R.id.tranding) {

            Data.strings=new Data().gett();
            Intent intent=new Intent(MainActivity.this,TreActivity.class);
            startActivity(intent);

        } else if (id == R.id.top) {

            Data.strings=new Data().getop();
            Intent intent=new Intent(MainActivity.this,TreActivity.class);
            startActivity(intent);
        }

        DrawerLayout drawer = (DrawerLayout) findViewById(R.id.drawer_layout);
        drawer.closeDrawer(GravityCompat.START);
        return true;
    }
}
--------------------------------------------------------------------------------------------------------
RecycleActivity
import android.Manifest;
import android.app.Dialog;
import android.app.DownloadManager;
import android.content.Context;
import android.content.Intent;
import android.content.pm.PackageManager;
import android.graphics.drawable.ColorDrawable;
import android.net.Uri;
import android.os.AsyncTask;
import android.os.Environment;
import android.support.annotation.Nullable;
import android.support.v4.app.ActivityCompat;
import android.support.v4.content.ContextCompat;
import android.support.v4.widget.SwipeRefreshLayout;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.support.v7.widget.DefaultItemAnimator;
import android.support.v7.widget.GridLayoutManager;
import android.support.v7.widget.RecyclerView;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageView;
import android.widget.RelativeLayout;
import android.widget.TextView;
import android.widget.Toast;

import com.google.android.gms.ads.AdListener;
import com.google.android.gms.ads.AdRequest;
import com.google.android.gms.ads.InterstitialAd;
import com.squareup.picasso.Picasso;

import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;

import java.util.ArrayList;

public class RecycleActivity extends AppCompatActivity {

    private ArrayList<Sample> strings = new ArrayList<>();
    private RecyclerView recyclerView;
    private MyAdapter mAdapter;
    SwipeRefreshLayout swipeRefreshLayout;
    private InterstitialAd mInterstitialAd;
    Sample fm;
    int bb=0;
    Dialog dialog;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_recycle);
        mInterstitialAd = new InterstitialAd(this);
        mInterstitialAd.setAdUnitId("ca-app-pub-3940256099942544/1033173712");
        mInterstitialAd.loadAd(new AdRequest.Builder().build());

        mInterstitialAd.setAdListener(new AdListener() {
            @Override
            public void onAdLoaded() {
                // Code to be executed when an ad finishes loading.
            }

            @Override
            public void onAdFailedToLoad(int errorCode) {
                // Code to be executed when an ad request fails.
            }

            @Override
            public void onAdOpened() {
                // Code to be executed when the ad is displayed.
            }

            @Override
            public void onAdLeftApplication() {
                // Code to be executed when the user has left the app.
            }

            @Override
            public void onAdClosed() {
                mInterstitialAd.loadAd(new AdRequest.Builder().build());
                if(bb==0) {
                    detail(fm);
                }else {
                    bb=0;
                    dialog.dismiss();
                }


            }
        });

        recyclerView = (RecyclerView) findViewById(R.id.recycler_view);
        swipeRefreshLayout=findViewById(R.id.swiperefresh);
        swipeRefreshLayout.setEnabled(false);



        mAdapter = new MyAdapter(strings);
        GridLayoutManager mGridLayoutManager =new GridLayoutManager(RecycleActivity.this, 1);

        recyclerView.setLayoutManager(mGridLayoutManager);
        recyclerView.setItemAnimator(new DefaultItemAnimator());
        recyclerView.setAdapter(mAdapter);

        new getJASONlist().execute();

    }

    public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {

        private ArrayList<Sample> mList;

        public class MyViewHolder extends RecyclerView.ViewHolder {
            public TextView title;
            public TextView size;
            public ImageView img;
            public RelativeLayout relative;

            public MyViewHolder(View view) {
                super(view);
                title = (TextView) view.findViewById(R.id.name);
                size = (TextView) view.findViewById(R.id.size);
                img = (ImageView) view.findViewById(R.id.imageView);
                relative= (RelativeLayout) view.findViewById(R.id.relative);


            }
        }


        public MyAdapter(ArrayList<Sample> mList) {
            this.mList = mList;
        }

        @Override
        public MyAdapter.MyViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
            View itemView = LayoutInflater.from(parent.getContext())
                    .inflate(R.layout.listitemrecycle, parent, false);

            return new MyAdapter.MyViewHolder(itemView);
        }

        @Override
        public void onBindViewHolder(MyAdapter.MyViewHolder holder, int position) {
           final Sample  m = mList.get(position);
            holder.title.setText(m.getSname());
            holder.size.setText(m.getSsize());
          //  holder.title.setText(m.getSname());
            Picasso.with(RecycleActivity.this).load(m.getSimg()).into(holder.img);
            holder.relative.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View view) {
                    fm=m;
                    if (mInterstitialAd.isLoaded()) {
                        mInterstitialAd.show();
                     bb=0;

                    } else {
                        detail(m);
                    }


                }
            });

        }

        @Override
        public int getItemCount() {
            return mList.size();
        }
    }


    void detail(final Sample sample){



        if (ContextCompat.checkSelfPermission(RecycleActivity.this,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)
                != PackageManager.PERMISSION_GRANTED) {
            if (ActivityCompat.shouldShowRequestPermissionRationale(RecycleActivity.this,
                    Manifest.permission.WRITE_EXTERNAL_STORAGE)) {

                ActivityCompat.requestPermissions(RecycleActivity.this,
                        new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                        10);

            } else {

                ActivityCompat.requestPermissions(RecycleActivity.this,
                        new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                        10);
            }
        }



        dialog=new Dialog(this,R.style.AppTheme);
        dialog.setCancelable(false);
        dialog.getWindow().getAttributes().windowAnimations = R.style.DialogAnimation_2;
        dialog.setContentView(R.layout.detaildilog);
        dialog.getWindow().setBackgroundDrawable(new ColorDrawable(getResources().getColor(R.color.black1)));

        ImageView imageView=dialog.findViewById(R.id.img);
        TextView name=dialog.findViewById(R.id.name);
        name.setText(sample.getSname());
        Picasso.with(RecycleActivity.this).load(sample.getSimg()).into(imageView);

        TextView download=dialog.findViewById(R.id.download);
        download.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                DownloadManage(sample.getSurl(),sample.getSname());

            }
        });

        TextView   close=dialog.findViewById(R.id.close);
        close.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                if (mInterstitialAd.isLoaded()) {
                    bb=1;
                    mInterstitialAd.show();
                } else {
                    bb=0;
                    dialog.dismiss();
                }


            }
        });
        TextView lic=dialog.findViewById(R.id.lic);
        lic.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                Intent i = new Intent(Intent.ACTION_VIEW);
                i.setData(Uri.parse(sample.getStime()));
                startActivity(i);

            }
        });
        dialog.show();




    }
    class getJASONlist extends AsyncTask<Void, Void, Void> {



        @Override
        protected void onPreExecute() {
            super.onPreExecute();
            swipeRefreshLayout.setRefreshing(true);

        }

        @Nullable
        @Override
        protected Void doInBackground(Void... params) {

            strings.clear();
            JSONObject object = DataParserObject.getDataFromWeb( Data.main.replace(" ","%20"));

            try {
                if (object != null) {
                    if (object.length() > 0) {
                        JSONArray array = object.getJSONArray("results");
                        int lenArray = array.length();
                        if (lenArray > 0) {
                            for (int jIndex = 0; jIndex < lenArray; jIndex++) {
                                JSONObject arrayJSONObject = array.getJSONObject(jIndex);
                                String name = arrayJSONObject.getString("name");
                                String artist_name = arrayJSONObject.getString("artist_name");
                                String album_image = arrayJSONObject.getString("album_image");
                                String audiodownload = arrayJSONObject.getString("audiodownload");
                                String duration = arrayJSONObject.getString("license_ccurl");
                                Sample sample=new Sample();
                                sample.setSname(name);
                                sample.setSurl(audiodownload);
                                sample.setSimg(album_image);
                                sample.setStime(duration);
                                sample.setSsize(artist_name);


                                strings.add(sample);
                            }
                        }
                    }
                } else {

                }
            } catch (JSONException je) {
                Log.i(DataParserObject.TAG, "" + je.getLocalizedMessage());

            }
            return null;
        }

        @Override
        protected void onPostExecute(Void aVoid) {
            super.onPostExecute(aVoid);
            mAdapter.notifyDataSetChanged();
            swipeRefreshLayout.setRefreshing(false);

        }
    }

    void DownloadManage(String url,String name){
        DownloadManager donwmanageer = (DownloadManager) getSystemService(Context.DOWNLOAD_SERVICE);
        Uri parse = Uri.parse(url);
        DownloadManager.Request downloadrequestmanage = new DownloadManager.Request(parse);
        downloadrequestmanage.setAllowedNetworkTypes(DownloadManager.Request.NETWORK_WIFI | DownloadManager.Request.NETWORK_MOBILE);
        downloadrequestmanage.setAllowedOverRoaming(false);
        downloadrequestmanage.setTitle(name);
        downloadrequestmanage.setDescription("Mp3 Downloading");
        downloadrequestmanage.allowScanningByMediaScanner();
        downloadrequestmanage.setNotificationVisibility(DownloadManager.Request.VISIBILITY_VISIBLE_NOTIFY_COMPLETED);
        downloadrequestmanage.setDestinationInExternalPublicDir(Environment.DIRECTORY_DOWNLOADS,name + ".mp3");
        donwmanageer.enqueue(downloadrequestmanage);
        Toast.makeText(RecycleActivity.this,"Your Downloading is starting in background please check in device notification bar",Toast.LENGTH_LONG).show();
    }

}
-------------------------------------------------------------------------------------------------------
Sample
public class Sample {
    String sname,ssize,stime,simg,surl;


    public Sample() {
    }

    public Sample(String sname, String ssize, String stime, String simg, String surl) {
        this.sname = sname;
        this.ssize = ssize;
        this.stime = stime;
        this.simg = simg;
        this.surl = surl;
    }

    public String getSname() {
        return sname;
    }

    public void setSname(String sname) {
        this.sname = sname;
    }

    public String getSsize() {
        return ssize;
    }

    public void setSsize(String ssize) {
        this.ssize = ssize;
    }

    public String getStime() {
        return stime;
    }

    public void setStime(String stime) {
        this.stime = stime;
    }

    public String getSimg() {
        return simg;
    }

    public void setSimg(String simg) {
        this.simg = simg;
    }

    public String getSurl() {
        return surl;
    }

    public void setSurl(String surl) {
        this.surl = surl;
    }
}
------------------------------------------------------------------------------------------------------
TreActivity
import android.Manifest;
import android.content.Intent;
import android.content.pm.PackageManager;
import android.support.v4.app.ActivityCompat;
import android.support.v4.content.ContextCompat;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.support.v7.widget.DefaultItemAnimator;
import android.support.v7.widget.GridLayoutManager;
import android.support.v7.widget.LinearLayoutManager;
import android.support.v7.widget.RecyclerView;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.TextView;

import com.google.android.gms.ads.AdListener;
import com.google.android.gms.ads.AdRequest;
import com.google.android.gms.ads.InterstitialAd;

import java.util.ArrayList;

public class TreActivity extends AppCompatActivity {


    private ArrayList<String> strings = new ArrayList<>();
    private RecyclerView recyclerView;
    private MyAdapter mAdapter;
    private InterstitialAd mInterstitialAd;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_tre);

        strings=Data.strings;
        mInterstitialAd = new InterstitialAd(this);
        mInterstitialAd.setAdUnitId("ca-app-pub-3940256099942544/1033173712");
        mInterstitialAd.loadAd(new AdRequest.Builder().build());

        mInterstitialAd.setAdListener(new AdListener() {
            @Override
            public void onAdLoaded() {
                // Code to be executed when an ad finishes loading.
            }

            @Override
            public void onAdFailedToLoad(int errorCode) {
                // Code to be executed when an ad request fails.
            }

            @Override
            public void onAdOpened() {
                // Code to be executed when the ad is displayed.
            }

            @Override
            public void onAdLeftApplication() {
                // Code to be executed when the user has left the app.
            }

            @Override
            public void onAdClosed() {
                mInterstitialAd.loadAd(new AdRequest.Builder().build());
                Intent intent=new Intent(TreActivity.this,RecycleActivity.class);
                startActivity(intent);

            }
        });
        recyclerView = (RecyclerView) findViewById(R.id.recycler_view);
        mAdapter = new MyAdapter(strings);
         GridLayoutManager mGridLayoutManager =new GridLayoutManager(TreActivity.this, 2);

        recyclerView.setLayoutManager(mGridLayoutManager);
        recyclerView.setItemAnimator(new DefaultItemAnimator());
        recyclerView.setAdapter(mAdapter);


        if (ContextCompat.checkSelfPermission(TreActivity.this,
                Manifest.permission.WRITE_EXTERNAL_STORAGE)
                != PackageManager.PERMISSION_GRANTED) {
            if (ActivityCompat.shouldShowRequestPermissionRationale(TreActivity.this,
                    Manifest.permission.WRITE_EXTERNAL_STORAGE)) {

                ActivityCompat.requestPermissions(TreActivity.this,
                        new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                        10);

            } else {
                ActivityCompat.requestPermissions(TreActivity.this,
                        new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                        10);
            }
        }
    }


















    public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {

        private ArrayList<String> mList;

        public class MyViewHolder extends RecyclerView.ViewHolder {
            public TextView title;

            public MyViewHolder(View view) {
                super(view);
                title = (TextView) view.findViewById(R.id.title);

            }
        }


        public MyAdapter(ArrayList<String> mList) {
            this.mList = mList;
        }

        @Override
        public MyViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
            View itemView = LayoutInflater.from(parent.getContext())
                    .inflate(R.layout.recyclelist, parent, false);

            return new MyViewHolder(itemView);
        }

        @Override
        public void onBindViewHolder(MyViewHolder holder, final int position) {
            String m = mList.get(position);
            holder.title.setText(m);
            holder.title.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View view) {
                    Data.main=mList.get(position);

                    if (mInterstitialAd.isLoaded()) {
                        mInterstitialAd.show();
                    } else {
                    Intent intent=new Intent(TreActivity.this,RecycleActivity.class);
                    startActivity(intent);
                    }
                }
            });

        }

        @Override
        public int getItemCount() {
            return mList.size();
        }
    }
}
============================================================================================================
activity_main
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"
    tools:openDrawer="start">



    <include
        layout="@layout/app_bar_main"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

    <android.support.design.widget.NavigationView
        android:id="@+id/nav_view"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:fitsSystemWindows="true"
        app:headerLayout="@layout/nav_header_main"
        app:menu="@menu/activity_main_drawer" />

</android.support.v4.widget.DrawerLayout>
------------------------------------------------------------------------------------------------------
activity_recycle
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.SwipeRefreshLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:id="@+id/swiperefresh"
    android:layout_height="match_parent"
    tools:context="com.game.admin.myapplication.RecycleActivity">

    <android.support.v7.widget.RecyclerView
        android:id="@+id/recycler_view"
        android:scrollbars="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</android.support.v4.widget.SwipeRefreshLayout>
------------------------------------------------------------------------------------------------------
activity_tre
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout

    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="4dp"
    android:background="@color/bg2"
    tools:context="com.game.admin.myapplication.TreActivity">
    <android.support.v7.widget.RecyclerView
        android:id="@+id/recycler_view"
        android:scrollbars="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</LinearLayout>
----------------------------------------------------------------------------------------------------
app_bar_main
<?xml version="1.0" encoding="utf-8"?>
<android.support.design.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.game.admin.myapplication.MainActivity">

    <android.support.design.widget.AppBarLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:theme="@style/AppTheme.AppBarOverlay">

        <android.support.v7.widget.Toolbar
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            android:background="?attr/colorPrimary"
            app:popupTheme="@style/AppTheme.PopupOverlay" />

    </android.support.design.widget.AppBarLayout>

    <include layout="@layout/content_main" />



</android.support.design.widget.CoordinatorLayout>
--------------------------------------------------------------------------------------------------------------
content_main
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
 android:orientation="vertical"
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/bg2"

    app:layout_behavior="@string/appbar_scrolling_view_behavior"
    tools:context="com.game.admin.myapplication.MainActivity"
    tools:showIn="@layout/app_bar_main">

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent">
        <LinearLayout
            android:orientation="vertical"
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <RelativeLayout
                android:padding="10dp"
                android:layout_width="match_parent"
                android:layout_height="wrap_content">

                <EditText
                    android:lines="1"
                    android:textColorHint="@color/colorPrimaryDark"
                    android:textColor="@color/colorPrimaryDark"
                    android:padding="10dp"
                    android:background="@drawable/shaper"
                    android:hint="Search Keyword"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:id="@+id/editText"
                    android:layout_toLeftOf="@+id/textView2"
                    android:layout_toStartOf="@+id/textView2" />

                <TextView

                    android:gravity="center"
                    android:background="@color/colorPrimary"
                    android:padding="10dp"
                    android:textStyle="bold"
                    android:textColor="#ffffff"
                    android:text="  GO  "
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_alignParentTop="true"
                    android:layout_alignParentRight="true"
                    android:layout_alignParentEnd="true"
                    android:layout_alignBottom="@+id/editText"
                    android:id="@+id/textView2" />



            </RelativeLayout>



            <RelativeLayout
                android:id="@+id/gener"
                android:layout_marginTop="10dp"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">


        <TextView
            android:padding="10dp"
            android:textStyle="bold"
            android:textColor="@color/colorPrimaryDark"
            android:text="MUSIC by GENRES"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />
        <TextView
            android:padding="10dp"
            android:textStyle="bold"
            android:textColor="@color/colorPrimary"
            android:text="MORE"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentTop="true"
            android:layout_alignParentRight="true"
            android:layout_alignParentEnd="true" />



    </RelativeLayout>

    <LinearLayout
        android:orientation="horizontal"
        android:weightSum="3"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <RelativeLayout
            android:layout_marginRight="5dp"
            android:layout_marginLeft="5dp"
            android:background="@color/text"
            android:layout_weight="1"
            android:id="@+id/img1"
            android:layout_width="0dp"
            android:layout_height="80dp">

            <TextView
                android:layout_margin="4dp"
                android:gravity="center"
                android:background="@drawable/bgr"
                android:text="POP ROCK"
                android:textStyle="bold"
                android:textColor="@color/text"
                android:textSize="18dp"
                android:layout_width="match_parent"
                android:layout_height="match_parent" />



        </RelativeLayout>

        <RelativeLayout
            android:layout_marginRight="5dp"
            android:layout_marginLeft="5dp"
            android:background="@color/text"
            android:layout_weight="1"
            android:id="@+id/img2"
            android:layout_width="0dp"
            android:layout_height="80dp">

            <TextView
                android:layout_margin="4dp"
                android:gravity="center"
                android:background="@drawable/bgr"
                android:text="POP"
                android:textStyle="bold"
                android:textColor="@color/text"
                android:textSize="18dp"
                android:layout_width="match_parent"
                android:layout_height="match_parent" />



        </RelativeLayout>
        <RelativeLayout
            android:layout_marginRight="5dp"
            android:layout_marginLeft="5dp"
            android:background="@color/text"
            android:layout_weight="1"
            android:id="@+id/img3"
            android:layout_width="0dp"
            android:layout_height="80dp">

            <TextView
                android:layout_margin="4dp"
                android:gravity="center"
                android:background="@drawable/bgr"
                android:text="ELEC.."
                android:textStyle="bold"
                android:textColor="@color/text"
                android:textSize="18dp"
                android:layout_width="match_parent"
                android:layout_height="match_parent" />



        </RelativeLayout>



    </LinearLayout>
    <LinearLayout
        android:layout_marginTop="10dp"
        android:orientation="horizontal"
        android:weightSum="3"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <RelativeLayout
            android:layout_marginRight="5dp"
            android:layout_marginLeft="5dp"
            android:background="@color/text"
            android:layout_weight="1"
            android:id="@+id/img4"
            android:layout_width="0dp"
            android:layout_height="80dp">

            <TextView
                android:layout_margin="4dp"
                android:gravity="center"
                android:background="@drawable/bgr"
                android:text="JAZZ"
                android:textStyle="bold"
                android:textColor="@color/text"
                android:textSize="18dp"
                android:layout_width="match_parent"
                android:layout_height="match_parent" />



        </RelativeLayout>

        <RelativeLayout
            android:layout_marginRight="5dp"
            android:layout_marginLeft="5dp"
            android:background="@color/text"
            android:layout_weight="1"
            android:id="@+id/img5"
            android:layout_width="0dp"
            android:layout_height="80dp">

            <TextView
                android:layout_margin="4dp"
                android:gravity="center"
                android:background="@drawable/bgr"
                android:text="ROCK"
                android:textStyle="bold"
                android:textColor="@color/text"
                android:textSize="18dp"
                android:layout_width="match_parent"
                android:layout_height="match_parent" />



        </RelativeLayout>
        <RelativeLayout
            android:layout_marginRight="5dp"
            android:layout_marginLeft="5dp"
            android:background="@color/text"
            android:layout_weight="1"
            android:id="@+id/img6"
            android:layout_width="0dp"
            android:layout_height="80dp">

            <TextView
                android:layout_margin="4dp"
                android:gravity="center"
                android:background="@drawable/bgr"
                android:text="CLASS.."
                android:textStyle="bold"
                android:textColor="@color/text"
                android:textSize="18dp"
                android:layout_width="match_parent"
                android:layout_height="match_parent" />



        </RelativeLayout>



    </LinearLayout>

            <RelativeLayout
                android:id="@+id/trending"
                android:layout_marginTop="10dp"
                android:orientation="vertical"
                android:layout_width="match_parent"
                android:layout_height="wrap_content">


                <TextView
                    android:padding="10dp"
                    android:textStyle="bold"
                    android:textColor="@color/colorPrimaryDark"
                    android:text="TRENDING MUSIC"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content" />
                <TextView
                    android:padding="10dp"
                    android:textStyle="bold"
                    android:textColor="@color/colorPrimary"
                    android:text="MORE"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_alignParentTop="true"
                    android:layout_alignParentRight="true"
                    android:layout_alignParentEnd="true" />



            </RelativeLayout>

            <LinearLayout
                android:orientation="horizontal"
                android:weightSum="3"
                android:layout_width="match_parent"
                android:layout_height="wrap_content">

                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img7"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="MAN"
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>

                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img8"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="WOMAN"
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>
                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img9"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="DJ"
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>



            </LinearLayout>
            <LinearLayout
                android:layout_marginTop="10dp"
                android:orientation="horizontal"
                android:weightSum="3"
                android:layout_width="match_parent"
                android:layout_height="wrap_content">

                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img10"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="TRUE"
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>

                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img11"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="REMIX"
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>
                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img12"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="POWER"
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>



            </LinearLayout>
            <RelativeLayout
                android:id="@+id/top"
              android:layout_marginTop="10dp"
                android:orientation="vertical"
                android:layout_width="match_parent"
                android:layout_height="wrap_content">


                <TextView
                    android:padding="10dp"
                    android:textStyle="bold"
                    android:textColor="@color/colorPrimaryDark"
                    android:text="TOP MUSIC"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content" />
                <TextView
                    android:padding="10dp"
                    android:textStyle="bold"
                    android:textColor="@color/colorPrimary"
                    android:text="MORE"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_alignParentTop="true"
                    android:layout_alignParentRight="true"
                    android:layout_alignParentEnd="true" />



            </RelativeLayout>

            <LinearLayout
                android:orientation="horizontal"
                android:weightSum="3"
                android:layout_width="match_parent"
                android:layout_height="wrap_content">

                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img13"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="SAD"
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>

                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img14"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="LOVE"
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>
                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img15"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="HAPPY"
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>



            </LinearLayout>
            <LinearLayout
                android:layout_marginTop="10dp"
                android:layout_marginBottom="20dp"
                android:orientation="horizontal"
                android:weightSum="3"
                android:layout_width="match_parent"
                android:layout_height="wrap_content">

                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img16"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="EMOTIONAL"
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>

                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img17"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="HIPHOP"
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>
                <RelativeLayout
                    android:layout_marginRight="5dp"
                    android:layout_marginLeft="5dp"
                    android:background="@color/text"
                    android:layout_weight="1"
                    android:id="@+id/img18"
                    android:layout_width="0dp"
                    android:layout_height="80dp">

                    <TextView
                        android:layout_margin="4dp"
                        android:gravity="center"
                        android:background="@drawable/bgr"
                        android:text="SOUNDT.."
                        android:textStyle="bold"
                        android:textColor="@color/text"
                        android:textSize="18dp"
                        android:layout_width="match_parent"
                        android:layout_height="match_parent" />



                </RelativeLayout>



            </LinearLayout>
        </LinearLayout>
    </ScrollView>

</LinearLayout>
----------------------------------------------------------------------------------------------------
detaildilog
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout

    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_gravity="center"
   android:layout_marginTop="40dp"
    android:background="@color/bg2"
    android:layout_marginBottom="40dp"
    android:layout_marginLeft="20dp"
    android:layout_marginRight="20dp"
    android:layout_height="match_parent">

    <RelativeLayout

        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerVertical="true"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"
        android:id="@+id/relativeLayout">

        <ImageView
            android:layout_marginTop="30dp"
        android:id="@+id/img"
        android:layout_width="150dp"
        android:layout_height="150dp"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true"
        android:scaleType="fitXY"
        android:src="@drawable/bgr" />

    <TextView
        android:gravity="center"
        android:layout_marginTop="10dp"
        android:layout_below="@+id/img"
        android:textSize="20dp"
        android:id="@+id/name"
        android:paddingRight="10dp"
        android:paddingLeft="10dp"
        android:textStyle="bold"
        android:text="Hello"
        android:textColor="@color/colorPrimaryDark"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        />

    <LinearLayout
        android:id="@+id/ll"
        android:layout_marginTop="40dp"
        android:padding="20dp"
        android:layout_below="@+id/name"
        android:orientation="horizontal"
        android:weightSum="2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <RelativeLayout
            android:layout_marginRight="5dp"
            android:layout_marginLeft="5dp"
            android:background="@color/text"
            android:layout_weight="1"
            android:id="@+id/img1"
            android:layout_width="0dp"
            android:layout_height="50dp">

            <TextView
                android:id="@+id/download"
                android:layout_margin="4dp"
                android:gravity="center"
                android:background="#D16A59"
                android:text="Download"
                android:textStyle="bold"
                android:textColor="@color/text"
                android:textSize="16dp"
                android:layout_width="match_parent"
                android:layout_height="match_parent" />



        </RelativeLayout>

        <RelativeLayout
            android:layout_marginRight="5dp"
            android:layout_marginLeft="5dp"
            android:background="@color/text"
            android:layout_weight="1"
            android:id="@+id/img2"
            android:layout_width="0dp"
            android:layout_height="50dp">

            <TextView
                android:id="@+id/lic"
                android:layout_margin="4dp"
                android:gravity="center"
                android:background="#D16A59"
                android:text="License"
                android:textStyle="bold"
                android:textColor="@color/text"
                android:textSize="16dp"
                android:layout_width="match_parent"
                android:layout_height="match_parent" />



        </RelativeLayout>




    </LinearLayout>


        <TextView

            android:id="@+id/close"
            android:layout_width="match_parent"
            android:layout_height="50dp"
            android:background="#D16A59"
            android:gravity="center"
            android:text="CLOSE"
            android:textColor="@color/text"
            android:textSize="16dp"
            android:textStyle="bold"
            android:layout_alignParentBottom="true"
            android:layout_alignParentLeft="true"
            android:layout_alignParentStart="true" />

    </RelativeLayout>


</RelativeLayout>
-----------------------------------------------------------------------------------------------------
listitemrecycle
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:background="@color/bg2"
    android:padding="4dp"
    android:layout_height="wrap_content">

    <RelativeLayout
        android:id="@+id/relative"
        android:padding="4dp"
        android:background="@color/text"
        android:layout_width="match_parent"
        android:layout_height="100dp"
        android:layout_alignParentTop="true"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true">



        <ImageView
            android:scaleType="fitXY"

            android:layout_width="100dp"
            android:layout_height="100dp"
            android:id="@+id/imageView" />

        <RelativeLayout
            android:layout_toRightOf="@+id/imageView"
            android:layout_toEndOf="@+id/imageView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

        <TextView
            android:lines="2"
            android:textSize="18dp"
            android:id="@+id/name"
            android:paddingRight="10dp"
            android:paddingLeft="10dp"
            android:textStyle="bold"
            android:text="Hello"
            android:textColor="@color/colorPrimaryDark"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            />

        <TextView
            android:layout_below="@+id/name"
            android:id="@+id/size"
            android:paddingRight="10dp"
            android:paddingLeft="10dp"
            android:textStyle="bold"
            android:text="Hello"
            android:textColor="#904C3434"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            />


        </RelativeLayout>


    </RelativeLayout>

</RelativeLayout>
----------------------------------------------------------------------------------------------------
nav_header_main
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="@dimen/nav_header_height"
    android:background="@drawable/bgr"
    android:gravity="center"
    android:orientation="vertical"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:theme="@style/ThemeOverlay.AppCompat.Dark">


    <TextView
        android:textSize="40dp"
        android:textStyle="bold"
        android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
       android:textColor="@color/text"
        android:text="Free \nMusic"
      />


</LinearLayout>
---------------------------------------------------------------------------------------------------
recyclelist
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:background="@color/bg2"
    android:padding="4dp"
    android:layout_height="wrap_content">


    <RelativeLayout

        android:background="@color/text"
        android:id="@+id/img1"
        android:layout_width="match_parent"
        android:layout_height="120dp">

        <TextView
            android:id="@+id/title"
            android:layout_margin="4dp"
            android:gravity="center"
            android:background="@drawable/bgr"
            android:text="HELLOW"
            android:textStyle="bold"
            android:textColor="@color/text"
            android:textSize="18dp"
            android:layout_width="match_parent"
            android:layout_height="match_parent" />



    </RelativeLayout>

</LinearLayout>
------------------------------------------------------------------------------------------------
test
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fitsSystemWindows="true"
    tools:openDrawer="start">

    <RelativeLayout
        android:padding="4dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <EditText
            android:padding="10dp"
            android:background="@drawable/shaper"
            android:hint="Search Keyword"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editText" />

        <TextView

            android:gravity="center"
            android:background="@color/colorPrimary"
            android:padding="10dp"
            android:textStyle="bold"
            android:textColor="#ffffff"
            android:text="  GO  "
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentTop="true"
            android:layout_alignParentRight="true"
            android:layout_alignParentEnd="true"
            android:layout_alignBottom="@+id/editText" />



    </RelativeLayout>


    <include
        layout="@layout/app_bar_main"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />



</android.support.v4.widget.DrawerLayout>
============================================================================================
