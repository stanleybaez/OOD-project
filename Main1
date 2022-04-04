import os
import mysql.connector
import hashlib
from functools import partial
from tkinter import *
from tkinter import simpledialog, ttk
from tkinter import ttk
from PIL import Image, ImageTk
import customtkinter

#Custom tkinter for Dark Mode Styling

customtkinter.set_appearance_mode("System")  # Modes: "System" (standard), "Dark", "Light"
customtkinter.set_default_color_theme("blue")  # Themes: "blue" (standard), "green", "dark-blue"

###############################Connect to database and create Members table#######################################

mydb = mysql.connector.connect(host='127.0.0.1',user='root', password='######')

cursor = mydb.cursor()
cursor.execute("""
USE GYM_DATABASE;
""")
cursor.execute("""
CREATE TABLE IF NOT EXISTS members(  
id int unsigned auto_increment not null,
first_name TEXT NOT NULL,
last_name TEXT NOT NULL,
DOB TEXT NOT NULL,
gender TEXT NOT NULL,
email TEXT NOT NULL,
phone TEXT NOT NULL,
address TEXT NOT NULL,
city TEXT NOT NULL,
state TEXT NOT NULL,
zip_code TEXT NOT NULL,
primary key (id));
""")


###############################Create the members window#######################################

root = customtkinter.CTk()
root.title('Main')
root.geometry("1160x600")

###############################Fetch all the data from the members table#######################################

def query_database():
    mydb = mysql.connector.connect(host='127.0.0.1',user='root', password='@Dany852456')
    cursor = mydb.cursor()
    cursor.execute("""
    USE GYM_DATABASE;
    """)
    cursor.execute("SELECT * FROM members")
    records = cursor.fetchall()
    global count 
    count =0

    for record in records:
        if count % 2 == 0:
            my_tree.insert(parent='', index = 'end', text='', values=(record[1],record[2],record[3],record[4],record[5],record[6],record[7],record[8],record[9],record[10]),tags=('evenrow',))
        else:
            my_tree.insert(parent='', index = 'end', text='', values=(record[1],record[2],record[3],record[4],record[5],record[6],record[7],record[8],record[9],record[10]),tags=('oddrow',))

        count += 1
    mydb.commit()
    mydb.close()

###############################Create the treeview frame to hold all data taken from the database table#######################################

style = ttk.Style()

style.theme_use('default')

style.configure("Treeview",
	background="#D3D3D3",
	foreground="black",
	rowheight=25,
	fieldbackground="#D3D3D3")

style.map('treeview', background = [('selected', "#347083")])

tree_frame = Frame(root)
tree_frame.pack(pady=10)

###############################assigning scrollbar to the treeview frame#######################################

tree_scroll = Scrollbar(tree_frame)
tree_scroll.pack(side=RIGHT, fill = Y)
tree_scroll1 = Scrollbar(tree_frame, orient='horizontal')
tree_scroll1.pack(side=BOTTOM, fill = X)

my_tree = ttk.Treeview(tree_frame, yscrollcommand=tree_scroll.set, xscrollcommand=tree_scroll1.set, selectmode="extended")
my_tree.pack()

tree_scroll.config(command=my_tree.yview)
tree_scroll1.config(command=my_tree.xview)

my_tree['columns']= ("First Name", "Last Name","DOB", "Gender", "Email","Phone", "Address", "City", "State", "Zip Code")

my_tree.column("#0", width=0, stretch=NO)
my_tree.column("First Name", anchor=W, width=140)
my_tree.column("Last Name", anchor=W, width=140)
my_tree.column("DOB", anchor=W, width=140)
my_tree.column("Gender", anchor=W, width=140)
my_tree.column("Email", anchor=W, width=140)
my_tree.column("Phone", anchor=W, width=140)
my_tree.column("Address", anchor=W, width=140)
my_tree.column("City", anchor=W, width=140)
my_tree.column("State", anchor=W, width=140)
my_tree.column("Zip Code", anchor=W, width=140)

my_tree.heading("#0", text="", anchor=W)
my_tree.heading("First Name", text="First Name", anchor=W)
my_tree.heading("Last Name", text="Last Name", anchor=W)
my_tree.heading("DOB", text="DOB", anchor=W)
my_tree.heading("Gender", text="Gender", anchor=W)
my_tree.heading("Email", text="Email", anchor=W)
my_tree.heading("Phone", text="Phone", anchor=W)
my_tree.heading("Address", text="Address", anchor=W)
my_tree.heading("City", text="City", anchor=W)
my_tree.heading("State", text="State", anchor=W)
my_tree.heading("Zip Code", text="Zip Code", anchor=W)


my_tree.tag_configure('oddrow', background="white")
my_tree.tag_configure('evenrow', background="lightblue")


###############################creating frame to hold the data entry for members#######################################

data_frame = customtkinter.CTkFrame(root)
data_frame.pack(fill="x", expand="yes", padx=20)

fn_label = customtkinter.CTkLabel(data_frame, text="first Name")
fn_label.grid(row=0, column=0, padx=10, pady=10)
fn_entry = customtkinter.CTkEntry(data_frame, placeholder_text = "first Name")
fn_entry.grid(row=0,column =1, padx=10, pady=10)

ln_label = customtkinter.CTkLabel(data_frame, text="Last Name")
ln_label.grid(row=0, column=2, padx=10, pady=10)
ln_entry = customtkinter.CTkEntry(data_frame, placeholder_text = "last Name")
ln_entry.grid(row=0,column =3, padx=10, pady=10)

dob_label = customtkinter.CTkLabel(data_frame, text="DOB")
dob_label.grid(row=0, column=4, padx=10, pady=10)
dob_entry = customtkinter.CTkEntry(data_frame, placeholder_text = "MM / DD / YYYY")
dob_entry.grid(row=0,column =5, padx=10, pady=10)

gender_label = customtkinter.CTkLabel(data_frame, text="Gender")
gender_label.grid(row=0, column=6, padx=10, pady=10)
gender_entry = customtkinter.CTkEntry(data_frame)
gender_entry.grid(row=0,column =7, padx=10, pady=10)

email_label = customtkinter.CTkLabel(data_frame, text="Email")
email_label.grid(row=1, column=0, padx=10, pady=10)
email_entry = customtkinter.CTkEntry(data_frame, placeholder_text = "you@yourmail.com")
email_entry.grid(row=1,column =1, padx=10, pady=10)

phone_label = customtkinter.CTkLabel(data_frame, text="Phone")
phone_label.grid(row=1, column=2, padx=10, pady=10)
phone_entry = customtkinter.CTkEntry(data_frame)
phone_entry.grid(row=1,column =3, padx=10, pady=10)

address_label = customtkinter.CTkLabel(data_frame, text="Address")
address_label.grid(row=2, column=0, padx=10, pady=10)
address_entry = customtkinter.CTkEntry(data_frame)
address_entry.grid(row=2,column =1, padx=10, pady=10)

city_label = customtkinter.CTkLabel(data_frame, text="City")
city_label.grid(row=2, column=2, padx=10, pady=10)
city_entry = customtkinter.CTkEntry(data_frame)
city_entry.grid(row=2,column =3, padx=10, pady=10)

state_label = customtkinter.CTkLabel(data_frame, text="State")
state_label.grid(row=2, column=4, padx=10, pady=10)
state_entry = customtkinter.CTkEntry(data_frame)
state_entry.grid(row=2,column =5, padx=10, pady=10)

zcode_label = customtkinter.CTkLabel(data_frame, text="Zip Code")
zcode_label.grid(row=2, column=6, padx=10, pady=10)
zcode_entry = customtkinter.CTkEntry(data_frame)
zcode_entry.grid(row=2,column =7, padx=10, pady=10)


###############################function to select records from a row #######################################

def select_record(e):
    fn_entry.delete(0, END)
    ln_entry.delete(0, END)
    dob_entry.delete(0, END)
    gender_entry.delete(0, END)
    email_entry.delete(0, END)
    phone_entry.delete(0, END)
    address_entry.delete(0, END)
    city_entry.delete(0, END)
    state_entry.delete(0, END)
    zcode_entry.delete(0, END)

    #Grab Records
    selected = my_tree.focus()

    values = my_tree.item(selected, 'values')

    fn_entry.insert(0, values[0])
    ln_entry.insert(0, values[1])
    dob_entry.insert(0, values[2])
    gender_entry.insert(0, values[3])
    email_entry.insert(0, values[4])
    phone_entry.insert(0, values[5])
    address_entry.insert(0, values[6])
    city_entry.insert(0, values[7])
    state_entry.insert(0, values[8])
    zcode_entry.insert(0, values[9])


###############################Function to remove a selected member#######################################

def remove_selection():
    x = my_tree.selection()[0]
    my_tree.delete(x)

    fname = fn_entry.get()
    lname = ln_entry.get()
    mydb = mysql.connector.connect(host='127.0.0.1',user='root', password='@Dany852456')
    cursor = mydb.cursor()
    cursor.execute("""
    USE GYM_DATABASE;
    """)
    val = (fname, lname)
    sql = "DELETE from members WHERE first_name= %s AND last_name= %s "

    cursor.execute(sql, val)


    mydb.commit()
    mydb.close()
    fn_entry.delete(0, END)
    ln_entry.delete(0, END)
    dob_entry.delete(0, END)
    gender_entry.delete(0, END)
    email_entry.delete(0, END)
    phone_entry.delete(0, END)
    address_entry.delete(0, END)
    city_entry.delete(0, END)
    state_entry.delete(0, END)
    zcode_entry.delete(0, END)

###############################function to update the records to the selected member#######################################

def update_record():
    selected = my_tree.focus()
    my_tree.item(selected, text="", values=(fn_entry.get(),ln_entry.get(),dob_entry.get(),gender_entry.get(),email_entry.get(),phone_entry.get(),address_entry.get(),city_entry.get(),state_entry.get(),zcode_entry.get() ))


    fname = fn_entry.get()
    lname = ln_entry.get()
    firstname = fn_entry.get()
    lastname = ln_entry.get()
    dob1 = dob_entry.get()
    gender = gender_entry.get()
    email = email_entry.get()
    phone = phone_entry.get()
    address = address_entry.get()
    city = city_entry.get()
    state = state_entry.get()
    zcode = zcode_entry.get()

    mydb = mysql.connector.connect(host='127.0.0.1',user='root', password='@Dany852456')
    cursor = mydb.cursor()
    cursor.execute("""
    USE GYM_DATABASE;
    """)

    val = (firstname, lastname, dob1, gender, email, phone, address, city, state, zcode, fname, lname)
    sql = """UPDATE members SET first_name = %s, last_name = %s, DOB = %s, gender = %s, email = %s, phone = %s, address = %s, city = %s, state = %s, zip_code = %s WHERE first_name= %s AND last_name= %s""" 

    cursor.execute(sql, val)

    


    mydb.commit()
    mydb.close()


    fn_entry.delete(0, END)
    ln_entry.delete(0, END)
    dob_entry.delete(0, END)
    gender_entry.delete(0, END)
    email_entry.delete(0, END)
    phone_entry.delete(0, END)
    address_entry.delete(0, END)
    city_entry.delete(0, END)
    state_entry.delete(0, END)
    zcode_entry.delete(0, END)

############################### Function to add a new member to the database and the treeview #######################################

def add_member():

    mydb = mysql.connector.connect(host='127.0.0.1',user='root', password='@Dany852456')
    cursor = mydb.cursor()
    cursor.execute("""
    USE GYM_DATABASE;
    """)

    fname = fn_entry.get()
    lname = ln_entry.get()
    dob = dob_entry.get()
    gender = gender_entry.get()
    email = email_entry.get()
    phone = phone_entry.get()
    address = address_entry.get()
    city = city_entry.get()
    state = state_entry.get()
    zipcode = zcode_entry.get()

    sql = """INSERT INTO members(first_name,last_name, DOB, gender, email, phone, address, city, state, zip_code)
            VALUES(%s,%s,%s,%s,%s,%s,%s,%s,%s,%s) """

    member_data = (fname,lname, dob, gender, email, phone, address, city, state, zipcode)
    cursor.execute(sql, member_data)
	


    mydb.commit()
    mydb.close()

    fn_entry.delete(0, END)
    ln_entry.delete(0, END)
    dob_entry.delete(0, END)
    gender_entry.delete(0, END)
    email_entry.delete(0, END)
    phone_entry.delete(0, END)
    address_entry.delete(0, END)
    city_entry.delete(0, END)
    state_entry.delete(0, END)
    zcode_entry.delete(0, END)

   
    my_tree.delete(*my_tree.get_children())

    query_database()


############################### Creating a frame to hold all the buttons for the above functions #######################################

button_frame = customtkinter.CTkFrame(root)
button_frame.pack(fill="x", expand="yes", padx=20)

update_button = customtkinter.CTkButton(button_frame, text="Update Selected Member", command=update_record)
update_button.grid(row=0,column=1, padx=10, pady=10)
add_button = customtkinter.CTkButton(button_frame, text="Add Member", command= add_member)
add_button.grid(row=0,column=0, padx=10, pady=10)
remove_button = customtkinter.CTkButton(button_frame, text="Delete Selected Member", command=remove_selection)
remove_button.grid(row=0,column=2, padx=10, pady=10)

my_tree.bind("<ButtonRelease-1>", select_record)


query_database()
root.mainloop()
