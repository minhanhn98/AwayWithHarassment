![alt text](https://github.com/minhanhn98/AwayWithHarassment/blob/master/Impact!.png "Impact! Logo")

#Table of Contents
[1.1 Impact! API Docuemtation](#11-impact-api-documentation)
[1.2 Getting Started With Impact!](#12-Getting-Started-With-Impact)
[2.1.1 Building a WebPage that uses Impact! API](#211-Building-a-WebPage-that-uses-Impact!)
[2.2.2 Sample code for submit entry](#222-Sample-code-for-submit-entry)
[2.3.1 Building an Android App that uses Impact!](#231-Building-an-Android-App-that-uses-Impact!)
[2.3.2 Sample code for submit entry](#232-Sample-code-for-submit-entry)

#1.1 Impact! API Documentation
What is Impact! API? Impact was made during the 2017 Hack UCSC event  in an attempt to build an API that could be very cross-platform and be able to filter inappropriate languages and output a positive message as a way to deter cyber bullies. 

##1.2 Getting Started With Impact!

Impact is actually fairly simple to implement and will start by showing how to implement it as a stand alone html form file. From there it is up to the user to find different ways to use the API. 

#2.1.1 Building a WebPage that uses Impact! API
Building a webpage that uses the Impact! API is as simple as having a text area somewhere on your webpage and having that submit via http POST. The following is one of the easiest examples and ways to send the http POST.

Note: Your webpage will want to be able to hand the .json file it will receive back or else you will end up with lots of files in your download list when testing out the code.

###2.2.2 Sample code for submit entry:

```html
<html>
<head>
<style> 
textarea {
    width: 100%;
    height: 150px;
    padding: 12px 20px;
    box-sizing: border-box;
    border: 2px solid #ccc;
    border-radius: 4px;
    background-color: #f8f8f8;
    font-size: 16px;
    resize: none;
}
</style>
</head>
<body>
<form action="http://impact-156315.appspot.com/impact_script" method="Post" name="UserForm">
<form> 								<form>
  <textarea name="UserSub" placeholder="Some text..."></textarea>
<input type="submit" value="Submit" >	
</form>

</body>
</html>
```

Take particular note at the url in the form tag with the method "Post". This url is where you will always be sending your form. You are going to want to handle the response using javascript or something like JQUERY. 

##2.3.1 Building an Android App that uses Impact! 

Now whenever you are working with Android applications there are certain things you are going to watch out for. A common mistake is running certain methods in the main activity. This will result in an error and your app may not run at all. But similar with a webpage, the main idea is having a text area form, and a button in order to submit the http POST request. Also, you are going to want to be making sure that you are sending the right format.

###2.3.2 Sample code for submit entry:
```
EditText msgText;
Button sendButton;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.form);
    
    msgTextField = (EditText) findViewById(R.id.msgTextField)
    sendButton = (Button) findViewById(R.id.sendButton);
}

public void send(View v) {
    String msg = msgTextField.getText().toString();
    if (!msg.isEmpty()) {
        new PostData().execute(msg);
    } else {
        Toast.makeText(getBaseContext(), "Submit...", Toast.LENGTH_SHORT).show();
    }
}

    public class PostData extends AsyncTask<String, Void, String> {
        @Override
        protected String doInBackground(String... params) {
            try {
                HttpClient httpclient = new DefaultHttpClient();
                HttpPost httppost = new HttpPost("http://impact-156315.appspot.com/impact_script");
                List<NameValuePair> nameValuePairs = new ArrayList<NameValuePair>(2);
                nameValuePairs.add(new BasicNameValuePair("id", "01"));
                nameValuePairs.add(new BasicNameValuePair("message", params[0]));
                httppost.setEntity(new UrlEncodedFormEntity(nameValuePairs));
                try {
                    HttpResponse response = httpclient.execute(httppost);
                    String op = EntityUtils.toString(response.getEntity(), "json");
                } catch (IOException e) {
                    e.printStackTrace();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }

            return null;
        }

        @Override
        protected void onPostExecute(String s) {
            super.onPostExecute(s);
            msgTextField.setText("");
            Toast.makeText(getBaseContext(), "Sent", Toast.LENGTH_SHORT).show();
        }
    }
 ```
    
Note: One of the first thing that happens is making the message text field object and creating the button. Remember that this can not happen in the main thread and must be done on a different one in the Android app.

#For a jQuery ajax POST to Impact!
Just for the simple request is not going to be too much work, but generally you have this associated with an action, if you just want the jQuery post() method and an example of it with the Impact! url, simply use the following code: 
```
$.ajax({
  type: "POST",
  url:http://impact-156315.appspot.com/impact_script ,
  data: String,
  success: success,
  dataType: json
});
```
But make sure that the value being sent is set to the name of "UserSub", if it is not, it may cause issues and will not return anything. You should get some kind of error stating that it is looking for another request.

#Working with Google Cloud Platform
The project used Python 3 for no other reason than the convenience of the developer, this proved to be quite a challenge as the Standard Environment for the Google App Engine only supported Python 2. So the decision was made to use the Flexable Environment. If you are unfamilar with the difference between the both of them, I suggest looking into the Google documentation. 


#Possible Reasons for Failure

In the case that you are receiving a 404, the server will not send back a 404, meaning there is something wrong with your application in the way you are sending it, or to where you are sending it to. If you copied in the url by hand please double check that it is correct. 

The data type is also very important, make sure it is always being sent as an http POST and the data being sent is form-data. 

A sanity check would be to test the api. An easy way to do this is to install the Chrome Extension [Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en), opening Postman, and doing the following:
<br />*Setting the method to POST
<br />*The URL to http://impact-156315.appspot.com/impact_script 
<br />*Clicking on Body then form-data 
<br />*Setting key to UserSub
<br />*Setting the value to your favorite curse word
<br />*Pressing Send

<br />*Finally... awaiting for a response. 

####If you receive back a curseword, congratulations! You found a bug in our program and should report it to us immediately so that we may update our dictionary as we are always looking to improve our API! E-mail us or contact us directly through our [Devpost](https://devpost.com/software/end-cyber-bullying). 

If you receive a word that is not a curse word, congratulations! You successfully communicated with the API! 
