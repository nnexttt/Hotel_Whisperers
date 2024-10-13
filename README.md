# MiniProject DADS5001
Mini-Project DADS5001 Data Analytics and Data Science Tools and Programming.
Project by 
1. 6620422010 ณฐกมลวรรณ แดงไพโรจน์
2. 6620422019 สุชานันท์ ยิ้มณรงค์
3. 6620422032 ถิรเดช เต็งวัฒนโชติ

# Source of Data
ชุดข้อมูลนี้ประกอบด้วยข้อมูลการจองสำหรับโรงแรมในเมืองและโรงแรมรีสอร์ท ในประเทศโปรตุเกส ตั้งแต่ปี 2015-2017

* Source: https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand/data 
* ชุดข้อมูลนี้ประกอบด้วยข้อมูลการจองสำหรับโรงแรมในเมืองและโรงแรมรีสอร์ท ซึ่งรวมถึงข้อมูลเช่น วันที่ทำการจอง ระยะเวลาการเข้าพัก จำนวนผู้ใหญ่ เด็ก และ/หรือทารก และจำนวนที่จอดรถที่มีอยู่ รวมถึงข้อมูลอื่นๆ
* ข้อมูลส่วนบุคคลที่สามารถระบุตัวตนได้ทั้งหมดได้ถูกลบออกจากชุดข้อมูลนี้แล้ว

# Reseach Question
1. ปัจจัยที่ส่งผลต่อยกเลิกการจองของโรงแรม
2. ช่วงเวลาหรือเดือนใดที่มีการยกเลิกการจองมากที่สุด?
3. ลูกค้าประเภทใดที่มีแนวโน้มจะทำการยกเลิกการจองมากที่สุด?
4. ราคาห้องพัก (ADR) มีผลต่อการยกเลิกการจองหรือไม่?
5. ช่องทางการจองแบบใดที่นิยมใช้ในการจองมากที่สุด?
6. อัตราการยกเลิกการจองในโรงแรมประเภทต่าง ๆ แตกต่างกันอย่างไร?

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
   กราฟแสดงจำนวนการจองแบบ Percentage ของลูกค้าภายในประเทศ กับ ลูกค้าต่างประเทศ ของโรงแรมแต่ละประเภท 
   ![Image](https://imgur.com/6qyGwvF.jpg)
   * # Question 1 ปัจจัยที่ส่งผลต่อยกเลิกการจองของโรงแรม  
     ตัวแปร
   ![image](https://imgur.com/kNDRU8Z.jpg)
   * 
