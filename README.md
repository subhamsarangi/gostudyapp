Native android app with just a WebView.

Features: The webview opens links of your specified domain and all the domains of links a tags the html pages, except youtube domains.

### MainActivity.java
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    this.webView = (WebView) findViewById(R.id.webview);
    WebSettings webSettings = webView.getSettings();
    webSettings.setJavaScriptEnabled(true);
    WebViewClientImpl webViewClient = new WebViewClientImpl(this);
    webView.setWebViewClient(webViewClient);
    webView.loadUrl("https://www.google.com"); // the url you want to open
}
```

### WebViewClientImpl.java
```java
@Override
public boolean shouldOverrideUrlLoading(WebView webView, String url) {
    if(url.indexOf("youtube.com") > -1 ){ // domain you dont want to open inside your webview
        Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse(url));
        activity.startActivity(intent);
        return true;
    }
    return false;
}
```
