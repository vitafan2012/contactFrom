var ss = SpreadsheetApp.getActiveSpreadsheet(),
sheet = ss.getSheetByName("sheet"); // "sheet1" 改成你的工作表名稱
var time = Utilities.formatDate(new Date(), "GMT", "yyyy/MM/dd HH:mm:ss");


function doPost(e) {
  var para = e.parameter, // 存放 post 所有傳送的參數
  method = para.method;

  if (method == "write") {
    write_data(para);
    sendEmail(para);
  }
  if (method == "read") {
  // 這裡放讀取資料的語法 下一篇說明
  }

}

function write_data(para) {
  var name = para.name,
      email = para.email,
      phone = para.phone,
      phone2 = '*'+ phone,
      country = para.country,
      city = para.city,
      message = para.message;
  sheet.appendRow([time, name, email, phone2, country, city, message]); // 插入一列新的資料
}



function sendEmail(datas) {
  var emailTo ='Q10@fiilex.com';
  var subject = "Fiilex Q10 Contact Form";

  var name = datas.name,
      email = datas.email,
      phone = datas.phone,
      country = datas.country,
      city = datas.city,
      message = datas.message;

  var html = "Timestamp:"+ time + '<br/> Name：' + name + '<br/> Email Address：' + email + '<br/> Phone：' + phone + '<br/> City:' + city + '<br/> Country:' + country + '<br/> Comments：' + message;
  
  GmailApp.sendEmail(emailTo, subject, html, {
    htmlBody: html
  });

  
}
