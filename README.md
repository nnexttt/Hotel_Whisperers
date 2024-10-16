# MiniProject DADS5001
Mini-Project DADS5001 Data Analytics and Data Science Tools and Programming.
Project by 
1. 6620422010 ณฐกมลวรรณ แดงไพโรจน์
2. 6620422019 สุชานันท์ ยิ้มณรงค์
3. 6620422032 ถิรเดช เต็งวัฒนโชติ

# Source of Data
ชุดข้อมูลนี้ประกอบด้วยข้อมูลการจองสำหรับโรงแรมในเมือง (City Hotel) และโรงแรมรีสอร์ท (Resort Hotel) ในประเทศโปรตุเกส ตั้งแต่ปี 2015-2017

* Source: https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand/data 
* ชุดข้อมูลนี้ประกอบด้วยข้อมูลการจองสำหรับโรงแรมในเมือง (City Hotel) และโรงแรมรีสอร์ท (Resort Hotel) ซึ่งรวมถึงข้อมูลเช่น วันที่ทำการจอง ระยะเวลาการจองล่วงหน้า ระยะเวลาการเข้าพัก จำนวนลูกค้าที่เป็นผู้ใหญ่ เด็ก และ/หรือทารก และจำนวนที่จอดรถที่มีอยู่ รวมถึงข้อมูลอื่นๆ
* ข้อมูลส่วนบุคคลที่สามารถระบุตัวตนได้ทั้งหมดได้ถูกลบออกจากชุดข้อมูลนี้แล้ว

# Reseach Question
1. ปัจจัยที่ส่งผลต่ออัตรายกเลิกการจองของโรงแรม
2. ช่วงฤดูกาลใดที่มีอัตราการยกเลิกการจองมากที่สุด?
3. ลูกค้าประเทศใดที่มีแนวโน้มจะทำการยกเลิกการจองมากที่สุด?
4. ปัจจัยที่ส่งผลต่อการเปลี่ยนแปลงของ Average daily rate (ADR)


# Data Jouney
1. Import library ที่ต้องใช้ในการวิเคราะห์ข้อมูล เช่น  
   * import pandas as pd  
import numpy as np  
import matplotlib.pyplot as plt  
import seaborn as sns  
import plotly.express as px  
import pycountry  
from sklearn.linear_model import LogisticRegression  
from sklearn.model_selection import train_test_split  
from sklearn.metrics import classification_report  
* Download Data Set ที่ต้องการวิเคราะห์โดยประกอบด้วยข้อมูลการจองสำหรับโรงแรมในเมืองและโรงแรมรีสอร์ท ตั้งแต่ปี 2015-2017 ที่ได้ download มาจาก Website Kaggle โดยข้อมูลทั้งหมดมีจำนวน 119390 rows และ 32 columns
  
2. Cleansing Data  
    ![image](https://imgur.com/Egy68Xb.jpg)  
   * จัดการ Column ที่มี missing data ทั้ง 4 column คือ  
   1.Country: จากข้อมูลประเทศที่เยอะที่สุดคือ ประเทศโปตุเกส(PRT) เราจึงใส่ค่า 'PRT' ลงไปในค่าเติมในค่า NaN     
   2.Children: จากข้อมูลจำนวน Children ที่เยอะที่สุดคือ 0 เราจึงใส่ค่า 0 ลงไปในค่าเติมในค่า NaN และสร้าง Colum ใหม่ชื่อ total_guest โดยรวม 'adults','children','babies' 
   3.Agent: ค่า NaN คือค่าที่ไม่มีรหัสของ Agent จึงสร้าง column ใหม่ ชื่อ is_agent และ แปลงค่าให้เป็น 0 (ไม่มี agent) และ 1 (มี agent) แทน  
   4.Company: ค่า NaN คือค่าที่ไม่มีรหัสของ Company จึงสร้าง column ใหม่ ชื่อ is_company และแปลงค่าให้เป็น 0 (ไม่มี company) และ 1 (มี company) แทน  
    * แปลงค่า column 'total_of_special_requests' และ 'required_car_parking_spaces' เป็นค่า 0 หรือ 1 
     
3. Data Analysis and Data Visualization  
   * กราฟแสดงจำนวนการจองของโรงแรมประเภท City Hotel กับ Resort Hotel
        
   ![Image](https://imgur.com/lY4UTji.jpg)

   * กราฟแสดงสถานะการจองห้องพัก
        
   ![Image](https://imgur.com/Imy69QP.jpg)  

 
   # Question 1 ปัจจัยที่ส่งผลต่อยกเลิกการจองของโรงแรม  
- is_local: ตัวแปรที่บ่งบอกว่าเป็นลูกค้าภายในประเทศหรือลูกค้าต่างประเทศ โดย is_local = 0 คือ ลูกค้าต่างประเทศ , is_local = 1 คือ ลูกค้าภายในประเทศ  
- is_agent: ตัวแปรที่บ่งบอกว่าเป็นลูกค้าที่จองผ่าน agent หรือไม่ โดย is_agent = 0 คือ ลูกค้าที่ไม่ได้จองผ่าน agent , is_agent = 1 คือ ลูกค้าที่จองผ่าน agent  
- is_company: ตัวแปรที่บ่งบอกว่าเป็นลูกค้าที่เป็นกลุ่มบริษัท หรือไม่ โดย is_company = 0 คือ ลูกค้าที่ไม่ใช่กลุ่มบริษัท , is_company = 1 คือ ลูกค้าที่เป็นกลุ่มบริษัท  
- is_spacial_request: ตัวแปรที่บ่งบอกว่าเป็นลูกค้าที่มีคำขอพิเศษหรือไม่ โดย is_spacial_request = 0 คือ ลูกค้าที่ไม่ได้ขอคำขอพิเศษ, is_spacial_request = 1 คือ ลูกค้าที่มีขอคำขอพิเศษ
- is_car_parking: ตัวแปรที่บ่งบอกว่าเป็นลูกค้าที่ต้องการที่จอดรถหรือไม่ โดย is_car_parking = 0 คือ ลูกค้าที่ไม่ต้องการที่จอดรถ , is_car_parking = 1 คือ ลูกค้าที่ต้องการที่จอดรถ  
- is_repeated_guest: ตัวแปรที่บ่งบอกว่าเป็นลูกค้าที่กลับมาใช้บริการซ้ำหรือไม่ โดย is_repeated_guest = 0 คือ ลูกค้าใหม่ , is_repeated_guest = 1 คือ ลูกค้าที่กลับมาใช้บริการซ้ำ  
- hotel_type: ตัวแปรที่บ่งบอกว่าเป็นโรงแรมประเภท Resort หรือ City โดย hotel_type = 0 คือ โรงแรมแบบ City Hotel, hotel_type = 1 คือ โรงแรมแบบ Resort Hotel  
* จากการใช้ Logistic Regression หาความสัมพันธ์ของ Binary Variables กับอัตราการยกเลิก (Cancellation Rate) จะเห็นได้ว่า column 'is_local'และ 'is_agent' มีความสัมพันธ์เชิงบวกกับ cancellation rate หมายความว่า 2 ตัวแปรนี้แปรผันตรงกับ cancellation rate  
   ส่วน column 'is_company', 'is_spacial_requests', 'is_car_parking', 'is_repeated_guest' และ 'hotel_type' มีความสัมพันธ์เชิงลบกับ cancellation rate หมายความว่า 5 ตัวแปรนี้แปรผกผันกับ cancellation rate  
     
   ![image](https://imgur.com/kNDRU8Z.jpg)  
     
* กราฟแสดงการเปรียบเทียบ Cancellation rate กับปัจจัยที่มาจาก Binary Variables  
   
  ![image](https://imgur.com/hEMwiFO.jpg)
  
* ด้านล่างเป็นกราฟ Correlation Between Factors and Cancellation จะแสดงความสัมพันธ์ของตัวแปรที่เป็นตัวเลข กับ cancellation rate จะเห็นได้ว่า ระยะเวลาการจองล่วงหน้า ('lead_time') ส่งผลต่อการอัตราการยกเลิกการจองมากที่สุด หมายความว่ายิ่งระยะเวลาการจองนาน ก็จะทำให้มีอัตราการยกเลิกสูง  
     
   ![image](https://imgur.com/S1jrOrQ.jpg)

* กราฟแสดงความสัมพันธ์ระหว่าง Lead time กับ Cancellation rate  
  ![image](https://imgur.com/TpANsQT.jpg)  
  
  จากกราฟอธิบายได้ว่า เห็นได้ว่าเมื่อ Lead Time เพิ่มขึ้นไปประมาณ 100-300 วัน อัตราการยกเลิกเริ่มมีการกระจายตัวและเพิ่มขึ้นอย่างต่อเนื่อง จากนั้นเมื่อ Lead Time เกินประมาณ 400 วัน อัตราการยกเลิกเริ่มมีการชะลอตัวลงและคงที่ในช่วง 500 วัน ขึ้นไป ดังนั้น หากต้องการจำกัด Lead Time เพื่อลดความเสี่ยงในการยกเลิก อาจพิจารณาให้ Lead Time ไม่เกิน 300-400 วัน เพราะหลังจากนั้นอัตราการยกเลิกจะมีแนวโน้มเพิ่มขึ้นตาม Trend Line ที่แสดงในกราฟ.
  
* กราฟแสดงการกระจายตัวของระยะเวลาการจองห้องพัก  
  ![image](https://imgur.com/gyPMqL2.jpg)  
  
  สรุปได้ว่าจากปัจจัยที่ส่งผลต่อการยกเลิกการจองห้องพัก พบว่าปัจจัยหลักที่ทำให้มีการยกเลิก คือ การจองที่มีระยะเวลาการจองล่วงหน้านานมักจะมีโอกาสยกเลิกมากกว่า จึงคิดว่าทางโรงแรมควรจำกัดระยะเวลาการจองให้น้อยลง เพื่อลดโอกาสในการยกเลิกการจอง และการตอบรับคำขอพิเศษจากลูกค้า spacial offer ต่างๆ รวมถึงมีที่จอดรถให้กับลูกค้าจะทำให้ตอบสนองความต้องการของลูกค้าได้ และส่งผลทำให้อัตราการยกเลิกการจองลดลงได้

  
  
# Question 2 ช่วงฤดูกาลใดที่มีอัตราการยกเลิกการจองมากที่สุด?
- High Season คือ เดือน มิถุนายน ถึง กันยายน จะเป็นช่วงฤดูร้อนของที่ประเทศโปรตุเกส ทำให้มีอากาสอบอุ่น เหมาะกับการเที่ยวชายหาดและกิจกรรมกลางแจ้ง
- Low Season คิอ เดือน พฤศจิกายน ถึง กุมภาพันธ์ เป็นฤดูหนาวและอากาศเย็น บางพื้นที่อาจจะหนาวถึงระดับหิมะ ช่วงนี้จะเป็นช่วงที่นักท่องเที่ยวไม่เยอะมาก ทำให้ค่าที่พัก และค่าตั่วเครื่องบินราคาถูกลง
- Shoulder Season คือเดือน มีนาคม ถึง พฤษภาคม และ กันยายน ถึง ตุลาคม เป็นช่วงเปลี่ยนผ่านฤดู ที่อากาศดีไม่ร้อนหรือไม่หนาวเกินไป  
* กราฟแสดงความสัมพันธ์ของ Cancellation Rate ตามฤดูกาล  
  ![image](https://imgur.com/8oglazQ.jpg)  
  จากกราฟแสดงให้เห็นว่า ช่วง High Season มีอัตราการยกเลิกสูง โดยอาจจะมีสาเหตุจากปัจจัยต่างๆดังต่อไปนี้  
  High Season มีการจองล่วงหน้านาน นอกจากนี้ ในช่วง High Season ยังมีลูกค้าที่กลับมาใช้บริการซ้ำ ('is_repeated_guest') น้อย จึงทำให้มีอัตราการยกเลิกสูง โดยสามารถดูกราฟเปรียบเทียบปัจจัยต่างๆ ในแต่ละฤดูกาลได้ด้านล่าง  

* กราฟแสดงการเปรียบเทียบของปัจจัยต่างๆ ในแต่ละฤดูกาล  
  ![image](https://imgur.com/GDV8Vpk.jpg)
  
    สรุปได้ว่า ช่วง High Season มีการจองล่วงหน้านาน และมีลูกค้าที่กลับมาใช้บริการซ้ำน้อย เป็นสาเหตุให้มีอัตราการยกเลิกสูง  
    โดยมีข้อเสนอแนะเพิ่มเติม คือ ในช่วง High Season ควรจะลดระยะเวลาการจองล่วงหน้าให้น้อยลง และเพิ่มโปรโมชั่นให้กับลูกค้าที่กลับมาพักที่โรงแรมซ้ำเพื่อดึงดูดลูกค้าเก่าให้มาเข้าพักมากขึ้น เช่น อัพเกรดห้องพัก และ Late Checkout โดยที่ไม่เสียค่าใช้จ่าย เพื่อที่จะลดอัตราการยกเลิกการจองห้องพักได้  
    
# Question 3 ลูกค้าประเทศใดที่มีแนวโน้มจะทำการยกเลิกการจองมากที่สุด?  
* จากภาพด้านล่าง เป็นแผนที่โลกแสดงอัตราการยกเลิกของแต่ละประเทศ โดยนับเพียงประเทศที่มีการจองตั้งแต่ 100 Booking ขึ้นไป โดยสามารถดู Top 10 ของประเทศที่มี Cancellation Rates สูงที่สุด จากกราฟแท่งด้านล่าง  
   ![Image](https://imgur.com/dvfRTZh.jpg)  
* จากภาพด้านล่าง จะเห็นได้ว่าประเทศที่มีการยกเลิกสูงสุดคือ ประเทศแองโกลา (AGO) อยู่ที่ 56.63%   
 ![Image](https://imgur.com/TpSL16z.jpg)  
สรุปได้ว่า กลุ่มประเทศที่กำลังพัฒนา มีอัตราการยกเลิกสูงกว่า กลุ่มประเทศที่พัฒนาแล้ว และเพื่อลดอัตราการยกเลิกจึงมีข้อเสนอแนะเกี่ยวกับนโยบายการยกเลิกการจองห้องพักให้ยืดหยุ่นมากขึ้น เช่น ยกเลิกภายในระยะเวลาที่กำหนด แต่ถ้าหากไม่ได้ยกเลิกภายในระยะเวลาดังกล่าวจะต้องเสียค่าธรรมเนียมการยกเลิก เป็นต้น

# Question 4 ปัจจัยที่ส่งผลต่อการเปลี่ยนแปลงของ Average daily rate (ADR)  
* กราฟแสดงการกระจายตัวของค่า Average daily rate (ADR)
![image](https://imgur.com/vlgumyT.jpg)  
จะเห็นได้ว่า ค่า Adr มีกระจายตัว โดยค่าเฉลี่ย = 101.98 ยูโร, SD = 50.42 ยูโร, median = 94.96 ยูโร  
กราฟมีลักษณะเบ้ขวา เนื่องจากค่า skewness = 10.62
  
*  จากการใช้ Logistic Regression หาความสัมพันธ์ของ Binary Variables ที่ส่งผลต่อค่า ADR จะเห็นได้ว่า column 'is_canceled', 'is_car_parking' และ 'is_repeated_guest' มีความสัมพันธ์เชิงบวกกับค่า ADR หมายความว่า 3 ตัวแปรนี้แปรผันตรงกับ ค่า ADR ส่วนตัวแปรที่ส่งผลเชิงลบต่อค่า ADR คือ 'is_local', 'is_agent', 'is_company', 'hotel_type' หมายความว่า 4 ตัวแปรนี้แปรผกผันกับ ค่า ADR เช่น hotel_type = 1 (Resort Hotel) แปลว่า Resort Hotel ราคาถูกกว่า City Hotel  
![image](https://imgur.com/RVX6t5W.jpg)  
  
* จากภาพด้านล่าง เป็นแผนที่โลกแสดงค่าเฉลี่ยของ ADR แต่ละประเทศ โดยนับเพียงประเทศที่มีการจองตั้งแต่ 100 Booking ขึ้นไป  
 ![image](https://imgur.com/wmufd1Z.jpg)
  
* กราฟแสดงค่าเฉลี่ย ADR ของ 50 ประเทศที่มีค่ามากที่สุด โดยค่าที่่มากที่สุดอยู่ที่ประเทศโมรอคโก (MAR)  
  ![image](https://imgur.com/gURqgtU.jpg)
    
* กราฟแสดงการกระจายตัวของค่า ADR ของแต่ละฤดูกาล  
 ![image](https://imgur.com/24Adg1H.jpg)  

  
* กราฟแสดงการเปรียบเทียบราคาห้องพักในแต่ละช่วงเวลา  
![image](https://imgur.com/QxnlJqy.jpg)
จากกราฟแสดงให้เห็นว่าค่า ADR ของโรงแรมประเภท Resort Hotel จะมีราคาสูงในช่วง High Season แต่ในฤดูกาลอื่นราคาจะถูกกว่า โรงแรมประเภท City Hotel โดยเฉลี่ยแล้วราคาที่พักของโรมแรมแบบ Resort Hotel จะถูกกว่าโรงแรมแบบ City Hotel  
  
  จากข้อมูลข้างต้นสามารถสันนิษฐานได้ว่า ปัจจัยที่ส่งผลต่อการเปลี่ยนแปลงค่า ADR คือ ประเทศของลูกค้า และปัจจัย 7 ปัจจัยดังนี้ 'is_canceled', 'is_car_parking', 'is_repeated_guest', 'is_local', 'is_agent', 'is_company', 'hotel_type' รวมถึงฤดูกาลด้วย  
  โดยมีข้อเสนอแนะเพิ่มเติม คือ การเพิ่มปัจจัยเชิงบวก และลดปัจจัยเชิงลบ เช่น เน้นกลุุ่มลูกค้าจากต่างประเทศ มีที่จอดรถให้กับลูกค้า และรองรับคำขอพิเศษจากลูกค้า และมีช่องทางการจองของโรงแรมโดยตรง เพื่อลดการจองจาก agent และเน้น Priority ลูกค้ากลุ่มอื่นๆ ก่อนกลุ่มลูกค้าที่เป็นบริษัท 






 
 
 
 
 


   
  
