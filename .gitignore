#coding=utf-8
'''
This programe make log-file of selecting dialog in Skype
'''
import sqlite3
import sys
def main():
    way = way_to_base_reading()
    conn = sqlite3.connect(way)
    c = conn.cursor()
    c.execute('select * from Messages')
    data = c.fetchall()
    contact = select_contact(data)
    log_contact = log(data, contact)
    write_file(log_contact, contact)
    conn.close()

def way_to_base_reading():
    '''
    Function to read the path from file config.py to the database file ofSkype (main.db)
    '''
    f = open('config.py')
    way = f.read()
    f.close()
    print way
    return way

def select_contact(data):
    '''
    Function make list of all contacts in Skype of user and write it for selection one of it
    '''
    all_contacts = []                   # list of all contacts in Skype
    for dat in data:
        if dat[8] not in all_contacts:
            all_contacts.append(dat[8])

    num = 0
    for dialog_partner in all_contacts:
        print num, ' ->', dialog_partner
        num +=1
    while True:
        contact = input('Choose your dialog_partner')
        print contact
        if contact in all_contacts: break
        if contact == 'Q' or contact == 'q':
            print 'Exiting now'
        else:
            print 'Input Error'
            exit()

    return contact

def log (data, contact):
    '''
    The function creates a list of lists, each containing information about a single message in
    the dialogue with the selected contact person Skype.
    Data consist of: [writing time, autor of message, text of messege]
    '''
    result = []
    for i in data:
        if i[8]==contact:
            print i[9], i[4], i[17]
            messege = []
            messege.append(i[9])
            messege.append(i[4])
            messege.append(i[17])
            result.append(messege)
    result = str(result)
    print('You search ', contact, ' for writing into file')
    return result

def write_file(data, contact):
    '''
    Creating of log-file in .txt format. Name of file consists of the selected User name
    of contact Skype and creating time it log-file. The file is created in the working directory.
    '''
    import datetime
    a = datetime.datetime.now()
    #contact = contact + '.txt'
    contact = contact + str(a.year) + str(a.month) + str(a.hour) + str(a.minute) + '.txt'
    print contact, ' - is your logfile name'
    f = open(contact, 'w')
    print data
    f.write(data)
    f.close()

if __name__ == '__main__':
    main()
