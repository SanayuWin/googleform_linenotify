# Google Forms Line Notify

คุณสามารถทำ Google Forms สำหรับส่ง line ตาม sciprt ด้านล่างได้ หรือ ศึกษาเพิ่มเติมได้ที่ https://notify-bot.line.me/doc/en/

```js
  
  function onFormSubmit(e) {
  
    var form = FormApp.openById('FORM ID'); 
    
    var formResponse = e.response;
    var itemResponse = formResponse.getItemResponses();

    for (var i = 0; i < itemResponse.length; i++) {
      var item = itemResponse[i];
      var itemName = item.getItem().getTitle();

      if (itemName.indexOf("message") > 0) {
        var messageForm = item.getResponse();
        sendLine(messageForm);
      }

    }
    
    function sendLine(message) {
      var url = 'https://notify-api.line.me/api/notify';
      var token = "Your token";

      var data = {
        "message": message
      }

      var options = {
        "method": "post",
        "headers": {
            "Authorization": "Bearer " + token,
            "Content-Type": "application/x-www-form-urlencoded",
        },
        "payload": data,
      };

      return UrlFetchApp.fetch(url, options);
    }

    sendLine();
  }

```

#### Thanks

Winny Freedom
