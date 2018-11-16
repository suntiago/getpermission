
# getpermission
## 解决Android 6.0+ 动态权限获取问题

## Step 1. 
Add the JitPack repository to your build file
Add it in your root build.gradle at the end of repositories:

	allprojects {
		repositories {
			...
			maven { url 'https://www.jitpack.io' }
		}
	}
## Step 2. 
Add the dependency

	dependencies {
	        implementation 'com.github.suntiago:getpermission:v1.0-beta'
	}
## Step 3.
request permission like this
```javascript
RxPermissions.getInstance(this).request(
                Manifest.permission.WRITE_EXTERNAL_STORAGE,
                Manifest.permission.READ_EXTERNAL_STORAGE,
                ACCESS_FINE_LOCATION,
                ACCESS_COARSE_LOCATION)
                .subscribe(new Action1<Boolean>() {
                    @Override
                    public void call(Boolean granted) {
                        if (granted) {
                            Toast.makeText(MainActivity.this, "权限已开启！", Toast.LENGTH_SHORT).show();
                        } else {
                            Toast.makeText(MainActivity.this, "请手动打开权限！", Toast.LENGTH_SHORT).show();
                            Intent intent = new Intent(Settings.ACTION_APPLICATION_DETAILS_SETTINGS);
                            intent.setData(Uri.parse("package:" + MainActivity.this.getPackageName()));
                            startActivity(intent);
                            finish();
                        }
                    }
```
