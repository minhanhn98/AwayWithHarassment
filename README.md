# Impact! API Documentation
What is Impact! API? Impact was made during the 2017 Hack UCSC event  in an attempt to build an API that could be very cross-platform and be able to filter inappropriate languages and output a positive message as a way to deter cyber bullies. 

#Getting Starting With Impact!

Impact is actually fairly simple to implement and will start by showing how to implement it as a stand alone html form file. From there it is up to the user to find different ways to use the API. 

#Building a WebPage that uses Impact! API
Building a webpage that uses the Impact! API is as simple as having a text area somewhere on your webpage and having that submit via http POST. The following is one of the easiest examples and ways to send the http POST.

Note: Your webpage will want to be able to hand the .json file it will receive back or else you will end up with lots of files in your download list when testing out the code.

Sample code for submit entry:

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
