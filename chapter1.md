# 登录:login

## Request

## Headers

![](/assets/import1.png)

### Text

![](/assets/import.png)

Password：加密算法---在com.youqianbao.credit.utils.f.class

```java
public static String a(String paramString)
  {
    if ((paramString == null) || (paramString.length() == 0)) {
      return "";
    }
    try
    {
      byte[] arrayOfByte = ("40bscE7guw1alwzrLzGk4yI6OD2lFHmgSMQGzjcP8cE" + paramString).getBytes("UTF-8");
      String str = new String(Base64.encode(arrayOfByte, 0, arrayOfByte.length, 0), "UTF-8");
      return str;
    }
    catch (UnsupportedEncodingException localUnsupportedEncodingException)
    {
      localUnsupportedEncodingException.printStackTrace();
    }
    return "";
  }
```

Header:com.yongqianbao.credit.common;

```java
public static Request a(String paramString1, String paramString2)
  {
    Request.Builder localBuilder1 = new Request.Builder();
    Request.Builder localBuilder2 = localBuilder1.url(paramString1).header("Version", com.yongqianbao.credit.utils.c.a(TinkerApplicationLike.getInstance().getContext()) + "").header("User-Agent", com.yongqianbao.credit.utils.c.b()).addHeader("ApiKey", "pILfaLRVfXhIArlpaVq5OBRzFXutWAT1ipmMe1FzZz0");
    String str1;
    if (TextUtils.isEmpty(TinkerApplicationLike.getInstance().getAuthCode())) {
      str1 = "";
    }
    for (;;)
    {
      Request.Builder localBuilder3 = localBuilder2.addHeader("AuthCode", str1).addHeader("Sign", paramString2);
      String str2;
      if (TextUtils.isEmpty(TinkerApplicationLike.getInstance().getFuckCode()))
      {
        str2 = "";
        localBuilder3.addHeader("SessionId", str2).addHeader("SystemInfo", TinkerApplicationLike.getInstance().getSystemInfo()).addHeader("Wid", TinkerApplicationLike.getInstance().getWid()).addHeader("A", TinkerApplicationLike.getInstance().getImei()).addHeader("B", TinkerApplicationLike.getInstance().getAndroidId()).addHeader("Host", "yongqianbao.daixiaomi.com");
      }
      try
      {
        localBuilder1.addHeader("Channel", j.v());
        return localBuilder1.build();
        str1 = TinkerApplicationLike.getInstance().getAuthCode();
        continue;
        str2 = TinkerApplicationLike.getInstance().getFuckCode();
      }
      catch (Exception localException)
      {
        for (;;)
        {
          j.u(com.yongqianbao.credit.utils.c.e(TinkerApplicationLike.getInstance().getContext()));
          localBuilder1.addHeader("Channel", com.yongqianbao.credit.utils.c.e(TinkerApplicationLike.getInstance().getContext()));
        }
      }
    }
```

其中apikey是一个特定的字符串：pILfaLRVfXhIArlpaVq5OBRzFXutWAT1ipmMe1FzZz0

Verdion:返回APP的版本号---/com/yongqianbao/credit/utils/c.class

```java
public static int a(Context paramContext)
  {
    try
    {
      int i = paramContext.getPackageManager().getPackageInfo(paramContext.getPackageName(), 0).versionCode;
      return i;
    }
    catch (Exception localException)
    {
      localException.printStackTrace();
    }
    return 0;
  }
```

AutoCode:/com/yongqianbao/credit/authenticator/a.class

```java
public static String b(Context paramContext)
  {
    try
    {
      AccountManager localAccountManager = AccountManager.get(paramContext);
      Account[] arrayOfAccount = localAccountManager.getAccountsByType(paramContext.getString(2131230747));
      if (arrayOfAccount.length > 0) {
        return localAccountManager.getUserData(arrayOfAccount[0], "authcode");
      }
      String str = j.k();
      return str;
    }
    catch (Exception localException) {}
    return j.k();
  }
```

Sign：组成：加密（“Phone=”+手机号）------/com/yongqianbao/credit/d/a/a.class

```java
public static m a(String paramString1, String paramString2)
    throws JSONException, IOException, ServerFailedException
  {
    String str1 = f.a(paramString2);
    for (;;)
    {
      JSONObject localJSONObject;
      synchronized (a)
      {
        a.clear();
        a.put("Phone", paramString1);
        a.put("Password", str1);
        String str2 = com.yongqianbao.credit.common.a.q;
        Map localMap2 = a;
        String[] arrayOfString = new String[1];
        arrayOfString[0] = ("Phone=" + paramString1);
        /*
        *************************下面一行是重点
        */
        localJSONObject = com.yongqianbao.credit.common.b.a(str2, localMap2, "/login", h.a(arrayOfString));
        
    }
  }
  h.a(arrayOfString))返回   加密（“Phone=”+手机号）
//加密算法如下
public static final String a(String paramString)
    throws NoSuchAlgorithmException
  {
    int i = 0;
    String str = "pILfaLRVfXhIArlpaVq5OBRzFXutWAT1ipmMe1FzZz0" + paramString;
    char[] arrayOfChar1 = { 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 97, 98, 99, 100, 101, 102 };
    byte[] arrayOfByte1 = str.getBytes();
    MessageDigest localMessageDigest = MessageDigest.getInstance("MD5");
    localMessageDigest.update(arrayOfByte1);
    byte[] arrayOfByte2 = localMessageDigest.digest();
    int j = arrayOfByte2.length;
    char[] arrayOfChar2 = new char[j * 2];
    int k = 0;
    while (i < j)
    {
      int m = arrayOfByte2[i];
      int n = k + 1;
      arrayOfChar2[k] = arrayOfChar1[(0xF & m >>> 4)];
      k = n + 1;
      arrayOfChar2[n] = arrayOfChar1[(m & 0xF)];
      i++;
    }
    return new String(arrayOfChar2);
  }
```

SessionID：

SystemInfo：/com/yongqianbao/credit/TinkerApplicationLike.class

```
public String getSystemInfo()
  {
    if (this.systemInfo == null)
    {
      String[] arrayOfString = new String[1];
      arrayOfString[0] = com.yongqianbao.credit.utils.c.d(this.context);
      this.systemInfo = h.a(arrayOfString);
    }
    return this.systemInfo;
  }
```

Wid：/com/yongqianbao/credit/TinkerApplicationLike.class

```java
public String getWid()
  {
    if ((!TextUtils.isEmpty(this.wid)) || (TextUtils.isEmpty(j.a()))) {}
    for (;;)
    {
      try
      {
        this.wid = h.a(getSystemInfo() + System.currentTimeMillis());
        j.a(this.wid);
        return this.wid;
      }
      catch (NoSuchAlgorithmException localNoSuchAlgorithmException)
      {
        localNoSuchAlgorithmException.printStackTrace();
        continue;
      }
      this.wid = j.a();
    }
  }
```

A：获取的是手机的IMEI值

/com/yongqianbao/credit/TinkerApplicationLike.class

```java
public String getImei()
  {
    if (TextUtils.isEmpty(this.imei)) {
      this.imei = com.yongqianbao.credit.utils.c.d(getApplication());
    }
    if (TextUtils.isEmpty(this.imei)) {
      return "";
    }
    return this.imei;
  }
```

B：获取的是设备ID（DEVICE\_ID）

/com/yongqianbao/credit/TinkerApplicationLike.class

```
public String getAndroidId()
  {
    if (TextUtils.isEmpty(this.androidId)) {
      this.androidId = m.c(getApplication());
    }
    return this.androidId;
  }
```

Channel

## Response

### json

![](/assets/import2.png)

# 登陆之后的启动界面

## Response

### JSON

![](/assets/import3.png)

## 个人信息界面

## Request

### Headers

![](/assets/import4.png)

## Response

### JOSN

Profile

![](/assets/import5.png)

AdditionInfo

![](/assets/import6.png)

