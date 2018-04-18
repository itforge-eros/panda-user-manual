บทที่ 3 การออกแบบฐานข้อมูล

3.1 แบบจำลองการออกแบบเชิงตรรกะ (Logical Design Model)


 
3.2 พจนานุกรมข้อมูล (Data Dictionary)

3.2.1 ตารางข้อมูลของฐานข้อมูล

|ชื่อตาราง|รายละเอียด|
|-|-|
|Equipment|เก็บข้อมูลอุปกรณ์ในสถานที่|
|SpaceEquipment|เก็บข้อมูลจำนวนของที่อยู่ในสถานที่|
|Space|เก็บข้อมูลสถานที่|
|SpaceType|เก็บข้อมูลประเภทของสถานที่|
|SpaceImage|เก็บข้อมูลรูปภาพของสถานที่|
|Group|เก็บข้อมูลสถานะหน้าที่ของคนในกลุ่มผู้ใช้งาน|
|RoleInclusion|เก็บข้อมูลกลุ่มของกลุ่มผู้ใช้|
|Problem|เก็บข้อมูลการแจ้งปัญหาภายในสถานที่|
|Request|เก็บข้อมูลการขอใช้งานสถานที่ที่ยังไม่ได้รับการอนุมัติ|
|Reservation|เก็บข้อมูลการใช้งานสถานที่|
|Approval|เก็บข้อมูลการยืนยันโดยผู้อนุมัติ|
|User|เก็บข้อมูลของผู้ใช้งาน|
|Permission|เก็บข้อมูลสิทธิของผู้ใช้งาน|
|UserRole|เก็บข้อมูลผู้ใช้งานที่อยู่ในกลุ่มหนึ่ง|
|RolePermission|เก็บข้อมูลสิทธิของผู้ใช้งานที่อยู่ในกลุ่ม|
|Role|เก็บข้อมูลกลุ่มของผู้ใช้งาน|

 
### 3.2.2 รายละเอียดข้อมูลในตาราง

#### พจนานุกรมข้อมูลของตาราง Equipment
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
|id|เป็น ID เฉพาะของอุปกรณ์แต่ละชี้น|UUID|PK|-|
|name|ชื่อของอุปกรณ์|VARCHAR	|-|-|

#### พจนานุกรมข้อมูลของตาราง SpaceEquipment
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
|space_id|เลขรหัสสถานที่ที่มีอุปกรณ์|UUID|PK FK|Space(id)|
|equipment_id|รหัสอุปกรณ์ที่อยู่ภายในห้อง|UUID|PK FK|Equipment(id)|
|quantity|จำนวนอุปกรณ์ที่อยู่ภายในสถานที่<br>เช่น ปากกาเขียนกระดาน 2 ชี้นในห้อง M03|INTEGER		|-|-|

#### พจนานุกรมข้อมูลของตาราง SpaceType
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
|id|เลขรหัสของสถานที่|UUID|PK|-|
|name|ประเภทของห้อง|VARCHAR		|-|-|

#### พจนานุกรมข้อมูลของตาราง Space
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
|id|เลขรหัสของสถานที่|UUID|PK|-|
|name|ชื่อสถานที่|VARCHAR|-|-|
|capacity|ความจุ หรือ จำนวนที่นั่งในสถานที่ / ห้อง|INT||
|required_approval|จำนวนผู้อนุมัติ |เพื่อการอนุมัติการใช้งานสถานที่|INT|-|-|		
|is_reservable|สถานที่สามารถจองได้หรือไม่|BOOLEAN|-|-|
|note|ข้อมูลเพิ่มเติมของสถานที่|TEXT|-|-|
|space_type_id|เลขรหัสของประเภทสถานที่|UUID|FK|SpaceType(id)|
|group_id|เลขกลุ่มที่สถานที่อยู่|UUID|FK|Group(id)|

#### พจนานุกรมข้อมูลของตาราง SpaceImage
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
|space_id|เลขรหัสของสถานที่|UUID|PK|-|
|url|File Path ของรูปภาพ|VARCHAR|PK|-|

#### พจนานุกรมข้อมูลของตาราง Problem
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
|id|เลข ID ของการแจ้งปัญหา|UUID|PK|-|
|title|ชื่อของปัญหา|VARCHAR|-|-|
|created_at|เวลาการส่งคำร้องของผู้ใช้งาน|TIMESTAMP|-|-|
|description|คำอธิบายของปัญหา|TEXT|-|-|
|space_id|เลข ID ของสถานที่ที่มีการแจ้งปัญหา|UUID|FK|Space(id)|
|user_id|เลข ID ของผู้แจ้งปัญหา|UUID|FK|User(id)|

#### พจนานุกรมข้อมูลของตาราง Group
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
|id|เลข ID ของกลุ่ม|UUID|PK|-|
|name|ชื่อของกลุ่ม|VARCHAR|-|-|
|description|คำอธิบายของกลุ่ม|TEXT|-|-|

#### พจนานุกรมข้อมูลของตาราง RoleInclusion
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
|role_id|เป็นเลข ID ของกลุ่มที่ทำหน้าที่เป็นกลุ่ม Superset|UUID|PK FK|Role(id)|
|child_role_id|เป็นเลข ID ของกลุ่มที่เป็น Subset ของอีกกลุ่ม|UUID|PK FK|Role(id)|

#### พจนานุกรมข้อมูลของตาราง Request
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
|id|เป็นเลขคำร้องขอใช้งานสถานที่|UUID|PK|
|purposal|เป็นข้อมูลคำร้องสถานที่ของผู้ใช้งาน|TEXT|||
|created_at|เวลาการสร้างคำร้อง|TIMESTAMP|||
|space_id|เป็น ID ของสถานที่ที่ต้องการขอใช้|UUID|FK|Space(id)|
|client_id|เป็น ID ของผู้ใช้งานที่ขอใช้งานสถานที่|UUID|FK|User(id)|

#### พจนานุกรมข้อมูลของตาราง Reservation
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
|id|เป็นเลขคำร้องที่ได้รับการอนุมัติแล้ว|UUID|PK|-|
|date|เป็นวันที่ต้องการใช้สถานที่|DATE|-|-|
|period|เป็นช่วงเวลาที่ต้องการใช้สถานที่|INT4RANGE|-|-|
|is_attended|เก็บข้อมูลว่าผู้ใช้งานเข้าใช้งานสถานที่แล้วหรือไม่|BOOL||EAN|-|-|
request_id|เป็นเลขของคำร้องที่ยังไม่ได้รับการอนุมัติ|UUID|FK|Reques||t(id)
พจนานุกรมข้อมูลของตาราง Approval
ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท |Key|Foreign| Key ที่ตาราง
|request_id|เป็นเลขคำร้องที่ยังไม่ได้รับการอนุมัติ|UUID|PK| |FK|Request(id)|
|approver_id|เป็น ID ของผู้อนุมัติ|VARCHAR|PK FK|Approver(id)|
|approved_at|เวลาที่ผู้อนุมัติทำการอนุมัติ|TIMESTAMP		|

#### พจนานุกรมข้อมูลของตาราง User
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
id	เป็นรหัสประจำตัวของผู้ใช้งาน	UUID	PK
first_name	ชื่อของผู้ใช้งาน	VARCHAR		
last_name	นามสกุลของผู้ใช้งาน	VARCHAR		
email	อีเมล์แอดเดรสของผู้ใช้	VARCHAR		

#### พจนานุกรมข้อมูลของตาราง Permission
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
id	เป็นเลขของสิทธ์	UUID	PK
name	ชื่อของสิทธิ	VARCHAR		
description	คำบรรยายของสิทธิ	VARCHAR		

#### พจนานุกรมข้อมูลของตาราง UserRole
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
user_id	เป็นรหัสประจำตัวของผู้ใช้งาน	UUID	PK FK	User(id)
role_id	เป็นเลขของหน้าที่ของผู้ใช้งาน	UUID	PK FK	Role(id)

#### พจนานุกรมข้อมูลของตาราง RolePermission
|ชื่อ attribute|หน้าที่ของ attribute|ประเภทข้อมูล|ประเภท Key|Foreign Key ที่ตาราง|
|-|-|-|-|-|
role_id	เป็นเลขของหน้าที่ของผู้ใช้งาน	UUID	PK FK	Role(id)
permission_id	เป็นเลขของสิทธ์	UUID	PK FK	Permission(id)
พจนานุกรมข้อมูลของตาราง Role
ชื่อ attribute	หน้าที่ของ attribute	ประเภทข้อมูล	ประเภท Key	Foreign Key ที่ตาราง
id	เป็นเลขของหน้าที่ของผู้ใช้งาน	UUID	PK
name	ชื่อของหน้าที่	VARCHAR		
description	คำอธิบายของหน้าที่	TEXT		
group_id	กลุ่มที่ผู้ใช้งานอยู่	UUID	FK	Group(id)

 
