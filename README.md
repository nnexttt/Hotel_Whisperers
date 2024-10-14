# MiniProject DADS5001
Mini-Project DADS5001 Data Analytics and Data Science Tools and Programming.
Project by 
1. 6620422010 ณฐกมลวรรณ แดงไพโรจน์
2. 6620422019 สุชานันท์ ยิ้มณรงค์
3. 6620422032 ถิรเดช เต็งวัฒนโชติ

# Source of Data
ชุดข้อมูลนี้ประกอบด้วยข้อมูลการจองสำหรับโรงแรมในเมืองและโรงแรมรีสอร์ท ในประเทศโปรตุเกส ตั้งแต่ปี 2015-2017

* Source: https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand/data 
* ชุดข้อมูลนี้ประกอบด้วยข้อมูลการจองสำหรับโรงแรมในเมืองและโรงแรมรีสอร์ท ซึ่งรวมถึงข้อมูลเช่น วันที่ทำการจอง ระยะเวลาการเข้าพัก จำนวนลูกค้าที่เป็นผู้ใหญ่ เด็ก และ/หรือทารก และจำนวนที่จอดรถที่มีอยู่ รวมถึงข้อมูลอื่นๆ
* ข้อมูลส่วนบุคคลที่สามารถระบุตัวตนได้ทั้งหมดได้ถูกลบออกจากชุดข้อมูลนี้แล้ว

# Reseach Question
1. ปัจจัยที่ส่งผลต่ออัตรายกเลิกการจองของโรงแรม
2. ช่วงฤดูกาลใดที่มีอัตราการยกเลิกการจองมากที่สุด?
3. ลูกค้าประเทศใดที่มีแนวโน้มจะทำการยกเลิกการจองมากที่สุด?
4. ปัจจัยที่ส่งผลต่อการเปลี่ยนแปลงของ Average daily rate (ADR)


# Data Jouney
1. Import library ที่ต้องใช้ในการวิเคราะห์ข้อมูล เช่น pandas,numpy และ matplotlib. Download dataset ที่ต้องการวิเคราะห์โดยประกอบด้วยข้อมูลการจองสำหรับโรงแรมในเมืองและโรงแรมรีสอร์ท ตั้งแต่ปี 2015-2017 ที่ได้ download มาจาก website Kaggle โดยข้อมูลทั้งหมดมีจำนวน 119390 rows และ 32 columns 
2. Cleansing Data  
    ![image](https://imgur.com/Egy68Xb.jpg)  
   * จัดการ Column ที่มี missing data ทั้ง 4 column คือ  
   1.Country: จากข้อมูลประเทศที่เยอะที่สุดคือ ประเทศโปตุเกส(PRT) เราจึงใส่ค่า 'PRT' ลงไปในค่าเติมในค่า null   
   2.Children: จากข้อมูลจำนวน Children ที่เยอะที่สุดคือ 0 เราจึงใส่ค่า 0 ลงไปในค่าเติมในค่า null และสร้าง Colum ใหม่ชื่อ total_guest โดยรวม 'adults','children','babies' เพื่อให้ง่ายต่อการวิเคราะห์  
   3.Agent: ค่า NaN คือค่าที่ไม่มีรหัสของ Agent จึงสร้าง column ใหม่ ชื่อ is_agent และ Normalize ค่าให้้เป็น 0 (ไม่มี agent) และ 1 (มี agent) แทน  
   4.Company: ค่า NaN คือค่าที่ไม่มีรหัสของ Company จึงสร้าง column ใหม่ ชื่อ is_company และ Normalize ค่าให้้เป็น 0 (ไม่มี company) และ 1 (มี company) แทน  
    * แปลงค่า column 'total_of_special_requests' และ 'required_car_parking_spaces' เป็นค่า 0 หรือ 1 เพื่อให้ง่ายต่อการวิเคราะห์  
   
3. Data Analysis and Data Visualization
   กราฟแสดงจำนวนการจองของโรงแรมประเภท City Hotel กับ Resort Hotel  
   ![Image](https://imgur.com/lY4UTji.jpg)

   กราฟแสดงสถานะการจองห้องพัก
   ![Image](https://imgur.com/Imy69QP.jpg)

 
   # Question 1 ปัจจัยที่ส่งผลต่อยกเลิกการจองของโรงแรม  
     จากการใช้ Logistic Regression หาความสัมพันธ์ของ Binary Variables กับอัตราการยกเลิก จะเห็นได้ว่า column 'is_local' และ 'is_agent' มีความสัมพันธ์เชิงบวกกับอัตราการยกเลิก หมายความว่า 2 ตัวแปรนี้แปรผันตรงกับ cancellation rate ส่วน column 'is_company', 'is_spacial_requests', 'is_car_parking', 'is_repeated_guest' และ 'hotel_type' มีความสัมพันธ์เชิงลบกับอัตราการยกเลิก หมายความว่า 5 ตัวแปรนี้แปรผกผันกับ cancellation rate
     
   ![image](https://imgur.com/kNDRU8Z.jpg)
กราฟแสดงการเปรียบเทียบ Cancellation rate กับปัจจัยที่มาจาก Binary Variables  
  ![image](https://imgur.com/hEMwiFO.jpg)

   ด้านล่างเป็นกราฟ Correlation Between Factors and Cancellation จะแสดงความสัมพันธ์์ของตัวแปรที่เป็นตัวเลข กับ cancellation rate จะเห็นได้ว่า ระยะเวลาการจองล่วงหน้า ('lead_time') ส่งผลต่อการอัตราการยกเลิกการจองมากที่สุด หมายความว่ายิ่งระยะเวลาการจองนาน ก็จะทำให้มีอัตราการยกเลิกสูง
     
   ![image](https://imgur.com/S1jrOrQ.jpg)

  * กราฟแสดงความสัมพันธ์ระหว่าง Lead time กับ Cancellation rate
  ![image](https://imgur.com/TpANsQT.jpg)

  จากกราฟอธิบายได้ว่า ข้อมูลมีความกระจายตัวสูง โดยเฉพาะในช่วง Lead Time ต่ำ (ประมาณ 0-200 วัน) ที่อัตราการยกเลิกมีทั้งสูงและต่ำ  
ในช่วง Lead Time สูง (เช่น 400 วันขึ้นไป) ข้อมูลมีแนวโน้มกระจุกตัวที่ค่า Cancellation Rate สูงกว่า 0.5 ซึ่งหมายความว่าการจองที่มีระยะเวลาล่วงหน้านานมักจะมีโอกาสยกเลิกมากกว่า  


# Question 2 ช่วงฤดูกาลใดที่มีอัตราการยกเลิกการจองมากที่สุด?
- High Season คือ เดือน มิถุนายน ถึง กันยายน จะเป็นช่วงฤดูร้อนของที่ประเทศโปรตุเกส ทำให้มีอากาสอบอุ่น เหมาะกับการเที่ยวชายหาดและกิจกรรมกลางแจ้ง
- Low Season คิอ เดือน พฤศจิกายน ถึง กุมภาพันธ์ เป็นฤดูหนาวและอากาศเย็น บางพื้นที่อาจจะหนาวถึงระดับหิมะ ช่วงนี้จะเป็นช่วงที่นักท่องเที่ยวไม่เยอะมาก ทำให้ค่าที่พักและเครื่องบินถูกลง
- Shoulder Season คือเดือน มีนาคม ถึง พฤษภาคม และ กันยายน ถึง ตุลาคม เป็นช่วงที่อากาศดีไม่ร้อนหรือไม่หนาวเกินไป
* กราฟแสดงความสัมพันธ์ของ Cancellation Rate ตามฤดูกาล  
  ![image](https://imgur.com/8oglazQ.jpg)
  จากกราฟแสดงให้เห็นว่า ช่วง High Season มีอัตราการยกเลิกสูง โดยอาจจะมีสาเหตุจากปัจจัยต่างๆดังต่อไปนี้
  High Season มีการจองล่วงหน้านาน นอกจากนี้ ในช่วง High Season ยังมีลูกค้าที่กลับมาใช้บริการซ้ำ ('is_repeated_guest') น้อย จึงทำให้มีอัตราการยกเลิกสูง
  
  ![image](https://imgur.com/GDV8Vpk.jpg)
  
    
# Question 3 ลูกค้าประเทศใดที่มีแนวโน้มจะทำการยกเลิกการจองมากที่สุด?  
* จากภาพด้านล่าง เป็นแผนที่โลกแสดงอัตราการยกเลิกของแต่ละประเทศ โดยนับเพียงประเทศที่มีการจองตั้งแต่ 100 Booking ขึ้นไป  
   ![Image](https://imgur.com/dvfRTZh.jpg)
* จากภาพด้านล่าง แสดง Top 10 ของประเทศที่มี Cancellation Rates สูงที่สุด โดยประเทศที่มีการยกเลิกสูงสุดคือ ประเทศแอฟริกาใต้ (AGO) อยู่ที่ 56.63%   
 ![Image](https://imgur.com/TpSL16z.jpg)

# Question 4 ปัจจัยที่ส่งผลต่อการเปลี่ยนแปลงของ Average daily rate (ADR)  
* กราฟแสดงการกระจายตัวของค่า Average daily rate (ADR)
![image](https://imgur.com/vlgumyT.jpg)  
จะเห็นได้ว่า ค่า Adr มีกระจายตัว โดยค่าเฉลี่ย = 101.98 ยูโร, SD = 50.42 ยูโร, median = 94.96 ยูโร  
กราฟมีลักษณะเบ้ขวา เนื่องจากค่า skewness = 10.62
  
*  จากการใช้ Logistic Regression หาความสัมพันธ์ของ Binary Variables ที่ส่งผลต่อค่า ADR จะเห็นได้ว่า column 'is_canceled', 'is_car_parking' และ 'is_repeated_guest' มีความสัมพันธ์เชิงบวกกับค่า ADR หมายความว่า 3 ตัวแปรนี้แปรผันตรงกับ ค่า ADR  
![image](https://imgur.com/RVX6t5W.jpg)
  
* จากภาพด้านล่าง เป็นแผนที่โลกแสดงค่าเฉลี่ยของ ADR แต่ละประเทศ โดยนับเพียงประเทศที่มีการจองตั้งแต่ 100 Booking ขึ้นไป  
 ![image](https://imgur.com/pzieTuI.jpg)

* กราฟแสดงค่าเฉลี่ย ADR ของ 50 ประเทศที่มีค่ามากที่สุด  
  โดยค่าที่่มากที่สุดอยู่ที่ประเทศโมรอคโก (MAR)  
  ![image](https://imgur.com/uHvDlaq.jpg)
  
* กราฟแสดงการกระจายตัวของค่า ADR ของแต่ละฤดูกาล  
 ![image](https://imgur.com/24Adg1H.jpg)  

* กราฟแสดงการเปรียบเทียบราคาห้องพักของโรงแรมแต่ละประเภท  
![image](https://imgur.com/QxnlJqy.jpg)



 
 
 
 
 


   
  
