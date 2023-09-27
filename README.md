# MEDICAL-STORE-MANAGEMENT-SYSTEM
import mysql.connector
con=mysql.connector.connect(host='Localhost',user='root',password='moumita',database='medicine_store')


def login():
    print("----------------------------------------------")
    print("                 MEDICINE SHOP")
    print("----------------------------------------------")
    print("1. Login")
    print("2. Exit")
    ch=input("Select your option:")
    if(ch=='1'):
        uid=input("Enter User ID : ")
        pwd=input("Enter Password : ")
        if ((uid=='abc') and (pwd=='123')):
            main()
    elif(ch=='2'):
        print("Exit")
    else:
        print("Invalid Choice")


def cust_add():
        cust_id = input("Enter Customer Id : ")
        cust_name = input("Enter Customer Name : ")
        phone = input("Enter Customer Phone Number : ")
        address = input("Enter Customer Address : ")

        data = (cust_id,cust_name,phone,address)
        sql = 'insert into customer values(%s,%s,%s,%s)'
        c = con.cursor()
        c.execute(sql,data)
        con.commit()
        print(">----------------------------------------------------------------------------------------<")
        print("Data Entered Successfully")
        main()
        
def cust_sear(cid):
        a = "select * from customer where cust_id="+cid+""
        c = con.cursor()
        c.execute(a)
        myresult = c.fetchall()
        for i in myresult:    
            print("Customer Id : ",i[0])
            print("Customer Name : ",i[1])
            print("Customer Phone : ",i[2])
            print("Customer Address : ",i[3])
            print(">--------------------------------<")
        main()


def supp_add():
        supp_id = input("Enter Supplier Id : ")
        supp_name = input("Enter Supplier Name : ")
        phone = input("Enter Supplier Phone Number : ")
        address = input("Enter Supplier Address : ")

        data = (supp_id,supp_name,phone,address)
        sql = 'insert into supplier values(%s,%s,%s,%s)'
        c = con.cursor()
        c.execute(sql,data)
        con.commit()
        print(">----------------------------------------------------------------------------------------<")
        print("Data Entered Successfully")
        main()
        
def supp_sear(sid):
        a = "select * from supplier where supp_id="+sid+""
        c = con.cursor()
        c.execute(a)
        myresult = c.fetchall()
        for i in myresult:    
            print("Supplier Id : ",i[0])
            print("Supplier Name : ",i[1])
            print("Supplier Phone : ",i[2])
            print("Supplier Address : ",i[3])
            print(">--------------------------------<")
        main()

def med_add():
        med_name = input("Enter Medicine Name : ")
        batch_no = input("Enter Batch Number : ")
        company = input("Enter Company Name : ")
        qty = input("Enter Quantity : ")
        price = input("Enter Price Per Unit : ")

        data = (med_name,batch_no,company,qty,price)
        sql = 'insert into medicine values(%s,%s,%s,%s,%s)'
        c = con.cursor()
        c.execute(sql,data)
        con.commit()
        print(">----------------------------------------------------------------------------------------<")
        print("Data Entered Successfully")
        main()
        
def med_sear(mname):
    
    a = "select * from medicine where med_name like '"+str(mname)+"'"
    c = con.cursor()
    c.execute(a)
    myresult = c.fetchall()
    for i in myresult:    
        print("Medicine Name : ",i[0])
        print("Batch Number : ",i[1])
        print("Company : ",i[2])
        print("Quantity : ",i[3])
        print("Price : ",i[4])
        print(">--------------------------------<")
    main()
    
def sell():
        
        cust_name = input("Enter Customer Name : ")
        doc_name= input("Enter Doctor Name: ")
        med_name=input("Enter Medicine Name: ")
        batch_no=input("Enter Batch Number: ")
        qty=int(input("Enter Quantity: "))
        unit_price=int(input("Enter Unit Price: "))
        net_price=qty*unit_price
        discount=(net_price*10)/100
        tot_price=net_price-discount
        sell_dt=input("Enter Date: ")
        data = (cust_name,doc_name,med_name,batch_no,qty,unit_price,net_price,discount,tot_price,sell_dt)
        sql = 'insert into sell values(%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)'
        c = con.cursor()
        c.execute(sql,data)
        con.commit()
        print(">----------------------------------------------------------------------------------------<")
        print("Data Entered Successfully")
        main()

def sell_sear():
    st_dt =input("Enter Starting Date : ")
    end_dt=input("Enter Ending Date: ")

    a = "select * from sell where sell_dt >='"+str(st_dt)+"' AND sell_dt <= '"+str(end_dt)+"'"
    c = con.cursor()
    c.execute(a)
    myresult = c.fetchall()
    for i in myresult:    
        print("Supplier Name"," ","Medicine Name"," ","Batch Number","  ","Quantity","  ","Unit Price","    ","Net Price"," ","Discount","  ","Total Price","   ","Date")
        print("-------------"," ","-------------"," ","------------","  ","--------","  ","----------","    ","---------"," ","--------","  ","-----------","   ","-------")
        print(   i[0],"   ",            i[1],"    ",        i[2],"    ",    i[3]," ",         i[4],"  ",          i[5],"   ",    i[6],"    ",     i[7],"   ",       i[8])
    main()
    
def monthly_purchase():
        st_dt =input("Enter Starting Date : ")
        end_dt=input("Enter Ending Date: ")

        a = "select * from purchase where pur_dt >='"+str(st_dt)+"' AND pur_dt <= '"+str(end_dt)+"'"
        c = con.cursor()
        c.execute(a)
        myresult = c.fetchall()
        for i in myresult:    
            print("Supplier Name"," ","Medicine Name"," ","Batch Number","  ","Quantity","  ","Unit Price","    ","Net Price"," ","Discount","  ","Total Price","   ","Date")
            print("-------------"," ","-------------"," ","------------","  ","--------","  ","----------","    ","---------"," ","--------","  ","-----------","   ","-------")
            print(   i[0],"   ",            i[1],"    ",        i[2],"    ",    i[3]," ",        i[4],"  ",         i[5],"   ",     i[6],"    ",    i[7],"   ",         i[8])
        main()

            
def main():
    print("---------------------")
    print("------ WELCOME ------")
    print("---------------------")
    print("1. Customer Add")
    print("2. Supplier Add")
    print("3. Entry Medicine")
    print("4. Sell")
    print("5. Search Customer Details")
    print("6. Search Supplier Details")
    print("7. Check Stock")
    print("8. Monthly Purcase Report")
    print("9. Monthly Sell Report")
    print("10. Exit")

    ch=input("Select your option : ")
    if(ch=='1'):
        cust_add()
    elif(ch=='2'):
        supp_add()
    elif(ch=='3'):
        med_add()
    elif(ch=='4'):
        sell()
    elif(ch=='5'):
        cid=input("Enter Customer ID : ")
        cust_sear(cid)
    elif(ch=='6'):
        sid=input("Enter Supplier ID : ")
        supp_sear(sid)
    elif(ch=='7'):
        mname=input("Enter Medicine Name : ")
        med_sear(mname)
    elif(ch=='8'):
        monthly_purchase()
    elif(ch=='9'):
        sell_sear()
    elif(ch=='10'):
        quit()
    else:
        print("Invalid Choice")

