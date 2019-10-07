# LaravelFormValidator

This library is used to validate the laravel form with ajax and verify the form data

# Dependency:
1. LaravelAjaxValidator.js (Required)
2. JQuery (Required)
3. Noty.js (Optional)
4. Add Csrf-token in header of your html page (Required any 1 of these two);
	- Add meta tag to your header
    ```
	<meta name="csrf-token" content="{{ csrf_token() }}">
    ```
   
	- (Highly Recomended) Create a function that return your csrf token dynamic if any request crash, dump or fail or when you debug your code
    ```
	public function refreshToken() {
	  session()->regenerate();
	  return response()->json([
	    "message" => 'Token Refreshed',
	    "token" => csrf_token()], 200);
	}

    ```
5. After validate the form in your controller use this return function:

    ```
    /**
     * Send return response when Ajax call on form submit
     * 
     * @param boolean   $cstatus    (Required)This will be true or false.
     * @param string    $curl       (Optional)This is the page Url where to redirect after form submit successfully.
     * @param string    $cmessage   (Optional)This is to show message on error. // This message is differenct from validation error message.
     * @param array     $cdata      (Optional)In case if you want to send some data in return.
     * @return array    This will return all param detail with array.
     * 
     * */
     
    public function sendResponse($cstatus, $curl = '', $cmessage = '', $cdata = []) {
        return [
            'status' => $cstatus,
            'url' => $curl,
            'message' => $cmessage,
            'data' => $cdata,
        ];
    }
    ```
    (Recomended to use upper code in parent controller and call a function like following code):
    ```
    return $this->sendResponse($status, $url, $message, $data)
    ```

# Uses:
1. Add LaravelAjaxValidator.js to your header.
2. setup library
```
    phpdev.setup({
        underfieldError: false,
        showBorderError: true,
        refreshCsrfToken: true,
        csrfTokenUrl: 'refreshToken', //this must be full url
        notifyError: true
    });
```
3. Add class '**ajaxForm**' to form tag.
3. done.

# Additional Feature:
 -Some time we need post request on href tag but we need to create form for that or write a ajax for that button to work as post request It can be easily done by simple define **data-method="Post"** in your href tag same as the code below, It will work as post.
 
```
<a href="yourUrl" data-method="post" >Click me</a>
```

# Advantage & Disadvantageg
 1. It can also validate laravel array value for validator.
 2. It cannot Submit file if there is file input in the form, you can add file name just like any input field. It will only send temporary file name.


# Options:

```
Param                               Default                             Description

debug                               false                                   As a developer for testing purpose it will return database error and any other error that occur when submit the form.
showBorderError                     true                                    It will show error if validation fail on any input field.
underfieldError                     true                                    It will show error under the input field in the span tag
notifyError                         false                                   This will show a noty popup when if any error occur
maxNoty                             1                                       This will show maximum number of notification at once
pleaseContactToAdmin                'Please contact admin for more info'    If debug is false and site is in development but still some error occur then it will show the default message
separateMessage                     false                                   If you want to show all message in different different noty then you can set this to true and increase max number of noty from one to higher number.
loaderClass                         'loader-div'                            When a form is validated by ajax it will take some time this is not good for front end user to wait so if you already have a loader added in your main layout then you can define your own here so the loder will show every time it check the form validation and loader will automatic hide when ajax is complete.
csrfTokenUrl                        null                                    If you already added the function from point 4.2 to refresh the token you can define the route here.
refreshCsrfToken                    false                                   If you want to refresh csrf token on every fail ajax.
```

<a href="https://paypal.me/hgphpdev" rel="some text">![Foo](https://github.com/hitugehlot22/LaravelFormValidator/blob/master/images.png?raw=true)</a>
