# Viết app sử dụng Android Studio
   + Android manifest.xml  => mô tả gì? app cần quyền để do-st: khai báo ntn? để làm gì?
   + vòng đời của 1 ứng dụng android.
     
     code tự sinh sau khi tạo 1 project: có sẵn hàm onCreate: tại sao???
   + Code: java language. 
     app cần check xem có quyền để do-st? : code ntn? ý nghĩa?
     
     giao diện: (res/layout) mô tả bằng file XML + UI Design review
     
        + thuộc tính text, hoặc các thuộc tính khác: giá trị hardcode => lưu vào nới khác, tham chiếu tới nó:
          
          cú pháp của việc tham chiếu là gì?
          
          ưu điểm của việc tham chiếu này?
          
          OS hỗ trợ auto việc lấy giá trị tham chiếu theo LOCATION, LANGUAGE, THEME  việc hỗ trợ auto này giúp app làm được điều gì?
          
        + đối tượng chứa: gộp các đối tượng con lại: cùng 1 quy luật sắp xếp để hiển thị
          
          các đối tượng con nằm kề nhau theo chiều dọc | hoặc ngang, gravity code tương tác với layout: vd hiển thị text
          
          mong muốn text hiển thị phù hợp với thiết lập LOCATION, LANGUAGE, THEME của người dùng thì làm ntn? (tránh hardcode)
          
     event (sự kiện) người dùng tác động vào app: CLICK vào button, click vào text,... với 1 sự kiện nào đó, muốn chạy 1 đoạn code để do-st  thì LAYTOUT cần làm gì?
     
              CODE viết như nào (2 cách)
---------------------------
     trong app có các thư mục đặc biệt: Assets
     
     khi sử dụng Window Explorer để copy các files + folder vào trong Assets
     
     thì khi compiler: mọi file này đều đi theo app, nằm trong app
     
     trong app có thể truy cập được đến các file này
     
     cú pháp truy cập vào là gì?
     
     lợi ích của việc app có sẵn các files (offline cũng có)?
     
     ứng dụng: app hướng dẫn việc X

==> tạo app1 sử dụng cơ chế Dữ liệu chuẩn bị trước trong Assets

         format dữ liệu: tuỳ ý, nội dung tuỳ ý
         
         công cụ để hiển thị dữ liệu: tuỳ ý
         
         có cần phải tiền xử lý trước khi hiển thị ko: tuỳ ý.
         
         SV TỰ ĐẶT RA VẤN ĐỀ => TỰ GIẢI QUYẾT VẤN ĐỀ
         
         MÔ TẢ ĐƯỢC DỮ LIỆU CÓ ĐẶC THÙ GÌ
         
                    DÙNG THUẬT TOÁN NÀO ĐỂ XỬ LÝ DỮ LIỆU (NẾU CẦN)

                    DÙNG ĐỐI TƯỢNG NÀO ĐỂ HIỂN THỊ DỮ LIỆU.
                    
                    (ĐỘ SÁNG TẠO LÀ KO GIỚI HẠN)
------------------------
APP2 (android studio):  tạo app tương đương với Mit App inventor

  app có 3 activity
  
  + activity1: about: about+nút gọi sang 2 activity còn lại
  + activity2: giải toán đơn giản (tuỳ ý). mỗi khi giải xong bài toán: gọi api tại https://k58kmt.tdh.io.vn/api  để gửi bài toán lên đó
    
    {app_by:mã số sv, input: {a:1,b:2,c:3,name:"hello tắc kè"},output:{ketluan:"vô nghiệm", abc:"xyz", nghiem:3.14}} nhận lại json: {ok:1, stt:1234}
    
  + activity3: 
    dùng web-view để truy cập từ  1 trang web https://k58kmt.tdh.io.vn?masv=mã sv của bạn

# BÀI LÀM
## 1.	Android manifest.xml
   
•	AndroidManifest.xml là file mô tả toàn bộ ứng dụng Android.

•	Khai báo:
o	Tên package của ứng dụng 
o	Các Activity 
o	Service 
o	Broadcast Receiver 
o	Content Provider 
o	Quyền (Permission) 
o	Phiên bản Android hỗ trợ 
o	Icon, Theme của app
•	Ví dụ:

<manifest>
   
    <uses-permission
    
        android:name="android.permission.CAMERA"/>
        
    <application>
    
        <activity
        
            android:name=".MainActivity">
            
            <intent-filter>
            
                <action

                    android:name="android.intent.action.MAIN"/>
                    
                <category
                
                    android:name="android.intent.category.LAUNCHER"/>
                    
            </intent-filter>
            
        </activity>
        
    </application>
    
</manifest>

•	Android bảo vệ dữ liệu người dùng.

     Muốn sử dụng:
     
o	Camera 
o	GPS 
o	Danh bạ 
o	Bộ nhớ 
o	Micro

       Thì phải xin quyền.
       
•	Ví dụ

<uses-permission
   
                   android:name="android.permission.CAMERA"/>
                   
•	Ý nghĩa: Cho phép ứng dụng truy cập Camera.

## 2.	Vòng đời (Lifecycle) của Activity
Vì:

•	Activity phải được khởi tạo trước khi chạy. 
•	Android Framework tự động gọi onCreate().
## 3.	App cần kiểm tra quyền (Permission)

    Từ Android 6.0 trở lên:
•	Không chỉ khai báo trong Manifest 
•	Phải xin quyền lúc chạy
-	Bước 1:  Manifest
  
<uses-permission
   
android:name="android.permission.CAMERA"/>

-	Bước 2:  Kiểm tra quyền
  
if(ContextCompat.checkSelfPermission(

                   this,
                   
                  Manifest.permission.CAMERA)
                  
                  != PackageManager.PERMISSION_GRANTED)
                  
            {
            
                   ActivityCompat.requestPermissions(
                   
                       this,
                       
                       new String[]{
                       
                              Manifest.permission.CAMERA
                              
                      },
                      
                     1);
                  }
•	Ý nghĩa
o	Checkselfpermission() : Kiểm tra đã có quyền chưa.
o	Requestpermissions() : Hiện hộp thoại xin quyền.

•	Giao diện Android

Ví dụ :

<Button
   
    android:id="@+id/btnLogin"
    
    android:layout_width="wrap_content"
    
    android:layout_height="wrap_content"
    
android:text="Đăng nhập"/>

o	UI Design : Android Studio hỗ trợ
o	Design : Kéo thả.
o	Code : Viết XML.
o	Split : Xem cả hai.
## 4.	Thuộc tính text, hoặc các thuộc tính khác: giá trị hardcode => lưu vào nới khác, tham chiếu tới nó:

•	Cú pháp của việc tham chiếu 
o	Cú pháp chung : @loai_tai_nguyen/ten_tai_nguyen
o	Tham chiếu String : android:text="@string/hello"
o	Tham chiếu Color : android:textColor="@color/red"
o	Tham chiếu Drawable (ảnh) : android:src="@drawable/logo"
o	Tham chiếu Kích thước (Dimension) android:textSize="@dimen/text_size"

•	Ưu điểm của việc tham chiếu : 
o	Dễ bảo trì
o	Tái sử dụng
o	Hỗ trợ đa ngôn ngữ
o	Hỗ trợ Theme
•	Os hỗ trợ auto việc lấy giá trị tham chiếu theo location, language, theme
OS tự lấy theo Language, Location, Theme

Ví dụ : 
o	values-en : 

<string name="hello">
   
    Hello
    
</string>

o	values-vi : 

<string name="hello">
   
    Xin chào
    
</string>

o	Code : android: text="@string/hello"
o	Người dùng đổi ngôn ngữ: 

English → Hello

Tiếng Việt → Xin chào

•	Việc hỗ trợ auto này giúp app làm được : 
o	Hỗ trợ nhiều quốc gia 
o	Hỗ trợ nhiều ngôn ngữ 
o	Hỗ trợ Dark Mode 
o	Không cần sửa code Java	
## 5.	Đối tượng chứa: gộp các đối tượng con lại: cùng 1 quy luật sắp xếp để hiển thị 
•	Các đối tượng con nằm kề nhau theo chiều dọc | hoặc ngang, gravity code tương tác với layout: vd hiển thị text

        Trong Android, Layout thường dùng để sắp xếp các View con theo chiều dọc hoặc chiều ngang.
        
o	Sắp xếp theo chiều dọc : Các đối tượng sẽ hiển thị từ trên xuống dưới.

<LinearLayout

    android:layout_width="match_parent"
   
    android:layout_height="match_parent"
    
    android:orientation="vertical">
    
    <TextView
    
        android:text="Họ tên"/>
        
    <Button
    
        android:text="Lưu"/>
        
</LinearLayout>

o	Sắp xếp theo chiều ngang : Các đối tượng sẽ hiển thị từ trái sang phải.

<LinearLayout
   
    android:layout_width="match_parent"
    
    android:layout_height="wrap_content"
    
    android:orientation="horizontal">
    
    <Button
    
        android:text="Có"/>
        
    <Button
       
        android:text="Không"/>
        
</LinearLayout>

o	Thuộc tính Gravity : Gravity dùng để căn chỉnh vị trí hiển thị của nội dung bên trong View 

hoặc Layout.

<TextView
    
    android:layout_width="match_parent"
   
    android:layout_height="wrap_content"
    
    android:text="Xin chào"
    
android:gravity="center"/>

o	Một số giá trị thường dùng:
-	Center 
-	Left 
-	Right 
-	Top 
-	Bottom 
-	Center_horizontal 
-	Center_vertical
•	Mong muốn text hiển thị phù hợp với thiết lập LOCATION, LANGUAGE, THEME của người dùng thì

làm ntn? (tránh hardcode)
       
         Trong Android không nên ghi trực tiếp văn bản vào mã nguồn hoặc giao diện vì sẽ gây khó 
         
         khăn khi thay đổi ngôn ngữ hoặc giao diện.
o	Lưu chuỗi trong strings.xml
-	File: res/values/strings.xml
-	Nội dung:
  
<resources>
   
   <string name="hello">Xin chào</string>

</resources>

Sử dụng: android:text="@string/hello" hoặc txtHello.setText(R.string.hello);

o	Hỗ trợ nhiều ngôn ngữ : 
-	Tạo nhiều thư mục tài nguyên:
  
res/values/

res/values-vi/

res/values-en/

  Ví dụ:
o	values-en/strings.xml : <string name="hello">Hello</string>
o	values-vi/strings.xml : <stringname="hello">Xinchào</string>

Android sẽ tự động hiển thị ngôn ngữ tương ứng với thiết lập của người dùng.

•	Tạo app1 sử dụng cơ chế Dữ liệu chuẩn bị trước trong Assets
o	Tạo file dữ liệu mẫu trong thư mục Assets (nganhhoc.json)
 

o	Xây dựng lớp Model NganhHoc.java để ánh xạ dữ liệu JSON
 



o	Giao diện màn hình tra cứu ngành học khi khởi động ứng dụng
 

o	Code đọc dữ liệu JSON từ thư mục Assets
 


o	Thuật toán phân tích (Parse) dữ liệu JSON bằng JSONArray
 



o	Thiết kế giao diện Activity chính bằng XML
 

o	Kết quả hiển thị danh sách ngành học sau khi xử lý dữ liệu

 	 




•	Tạo app 2(android studio): tạo app tương đương với Mit App inventor
o	Giao diện thiết kế Activity About trong Android Studio
 

 







o	Thiết kế giao diện Activity About và điều hướng Activity
 

o	Giao diện Activity Giải Toán
 





o	Thiết kế Activity WebView
 

o	Khai báo sự kiện chuyển Activity trong MainActivity
 




o	Xây dựng chức giải toán và xử lý dữ liệu
 

o	Tích hợp API gửi kết quả bài toán bằng Retrofit/Volley

 





o	Xử lý phản hồi JSON từ Server
 

o	Kết quả chạy Activity About trên thiết bị Android
 
o	Kết quả chạy Activity Giải Toán và hiển thị kết quả
 





o	Kết quả chạy Activity WebView truy cập web https://k58kmt.tdh.io.vn?masv=K225480106038
 






