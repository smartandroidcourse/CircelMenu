<ol dir="auto">
<li>
<p dir="auto">Include the library as local library project:</p>
<div class="highlight highlight-source-groovy notranslate position-relative overflow-auto" dir="auto">
<pre><code id="depCodeGradle" class=" kode  language-css">maven <span class="token string">{url 'https://jitpack.io'}</span></code><span class="pl-s"><span class="pl-pds"><br /><br /></span></span></pre>
</div>
</li>
<li>
<p dir="auto">Include the library as local library project:</p>
<div class="highlight highlight-source-groovy notranslate position-relative overflow-auto" dir="auto">
<pre><code id="depCodeGradle" class=" kode  language-css">implementation <span class="token string">'com.github.smartandroidcourse:CircelMenu:1.0</span></code><span class="pl-s"><span class="pl-pds">'<br /><br /></span></span></pre>
</div>
</li>
<li>
<p dir="auto">Values: (<strong>arrays.xml</strong>)</p>
<div class="highlight highlight-source-groovy notranslate position-relative overflow-auto" dir="auto">
<pre><code id="depCodeGradle" class=" kode  language-css">&lt;resources&gt;<span class="token string">
    &lt;array name="icons"&gt;
        &lt;item&gt;@drawable/ic_home&lt;/item&gt;
        &lt;item&gt;@drawable/ic_person&lt;/item&gt;
        &lt;item&gt;@drawable/ic_settings&lt;/item&gt;
       &lt;item&gt;@drawable/ic_notifications&lt;/item&gt;
        &lt;item&gt;@drawable/ic_place&lt;/item&gt;
    &lt;/array&gt;
   &lt;array name="colors"&gt;
        &lt;item&gt;@android:color/holo_blue_light&lt;/item&gt;
        &lt;item&gt;@android:color/holo_green_dark&lt;/item&gt;
        &lt;item&gt;@android:color/holo_red_light&lt;/item&gt;
        &lt;item&gt;@android:color/holo_purple&lt;/item&gt;
        &lt;item&gt;@android:color/holo_orange_light&lt;/item&gt;
    &lt;/array&gt;
&lt;/resources&gt;</span></code><span class="pl-s"><span class="pl-pds"><br /><br /></span></span></pre>
</div>
</li>
<li>
<p dir="auto">Add view to your layout file:</p>
<div class="highlight highlight-text-xml notranslate position-relative overflow-auto" dir="auto">
<pre><span class="pl-c"><span class="pl-c">&lt;!--</span> ... <span class="pl-c">--&gt;</span></span></pre>
<pre>&lt;?xml version="1.0" encoding="utf-8"?&gt;<br />&lt;FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"<br />    android:layout_width="match_parent"<br />    android:layout_height="match_parent"<br />    xmlns:app="http://schemas.android.com/apk/res-auto"<br />    android:background="@android:color/white"&gt;<br /><br />    &lt;colorsfx.smart.android.courses.circlemenu.CircleMenuView<br />        android:id="@+id/circle_menu"<br />        android:layout_width="wrap_content"<br />        android:layout_height="wrap_content"<br />        app:button_colors="@array/colors"<br />        app:button_icons="@array/icons"<br />        android:layout_gravity="center"/&gt;<br /><br />&lt;/FrameLayout&gt;</pre>
<pre><span class="pl-c"><span class="pl-c">&lt;!--</span> ... <span class="pl-c">--&gt;</span></span></pre>
<div class="zeroclipboard-container position-absolute right-0 top-0">&nbsp;</div>
</div>
</li>
<li>
<p dir="auto">Add component handler into your activity or fragment (<strong>Java</strong>):</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto">
<pre>public class MainActivity extends AppCompatActivity {<br /><br />    private DayNightSwitch day_night_switch;<br />    public static final String TAG = "MainActivity";<br /><br />    @Override<br />    protected void onCreate(Bundle savedInstanceState) {<br />        super.onCreate(savedInstanceState);<br />        setContentView(R.layout.activity_main);<br /><br />        final View background_view = findViewById(R.id.background_view);<br /><br />        day_night_switch = (DayNightSwitch)findViewById(R.id.day_night_switch);<br />        day_night_switch.setDuration(450);<br /><br />        day_night_switch.setListener(new DayNightSwitchListener() {<br />            @Override<br />            public void onSwitch(boolean is_night) {<br />                Log.d(TAG, "onSwitch() called with: is_night = [" + is_night + "]");<br />                if (is_night)<br />                    background_view.setAlpha(1f);<br /><br />            }<br />        });<br /><br />        day_night_switch.setAnimListener(new DayNightSwitchAnimListener() {<br />            @Override<br />            public void onAnimStart() {<br />                Log.d(TAG, "onAnimStart() called");<br />            }<br /><br />            @Override<br />            public void onAnimEnd() {<br />                Log.d(TAG, "onAnimEnd() called");<br />            }<br /><br />            @Override<br />            public void onAnimValueChanged(float value) {<br />                background_view.setAlpha(value);<br />                Log.d(TAG, "onAnimValueChanged() called with: value = [" + value + "]");<br />            }<br />        });<br /><br />    }<br /><br /><br />}</pre>
<div class="zeroclipboard-container position-absolute right-0 top-0">&nbsp;</div>
</div>
</li>
<li>
<p dir="auto">Add component handler into your activity or fragment (<strong>Kotlin</strong>):</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto">
<pre>class MainActivity : AppCompatActivity() {<br /><br />    override fun onCreate(savedInstanceState: Bundle?) {<br />        super.onCreate(savedInstanceState)<br />        setContentView(R.layout.activity_main)<br /><br />        val menu = findViewById&lt;View&gt;(R.id.circle_menu) as CircleMenuView<br />        menu.eventListener = object : CircleMenuView.EventListener() {<br />            override fun onMenuOpenAnimationStart(view: CircleMenuView) {<br />                Log.d("D", "onMenuOpenAnimationStart")<br />            }<br /><br />            override fun onMenuOpenAnimationEnd(view: CircleMenuView) {<br />                Log.d("D", "onMenuOpenAnimationEnd")<br />            }<br /><br />            override fun onMenuCloseAnimationStart(view: CircleMenuView) {<br />                Log.d("D", "onMenuCloseAnimationStart")<br />            }<br /><br />            override fun onMenuCloseAnimationEnd(view: CircleMenuView) {<br />                Log.d("D", "onMenuCloseAnimationEnd")<br />            }<br /><br />            override fun onButtonClickAnimationStart(view: CircleMenuView, index: Int) {<br />                Log.d("D", "onButtonClickAnimationStart| index: $index")<br />            }<br /><br />            override fun onButtonClickAnimationEnd(view: CircleMenuView, index: Int) {<br />                Log.d("D", "onButtonClickAnimationEnd| index: $index")<br />            }<br />        }<br /><br />    }<br /><br />    }<br /><br /></pre>
<div class="zeroclipboard-container position-absolute right-0 top-0">&nbsp;</div>
</div>
</li>
</ol>
