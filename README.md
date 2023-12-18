
"""
Created on Wed Nov 22 09:26:30 2023

@author: motazsirriyeh
"""

class Office:
    def __init__(self, office_number, office_name):
        self.office_number = office_number
        self.office_name = office_name
        self.employees = []

    def addEmployee(self, employee_name):
        if employee_name not in self.employees:
            self.employees.append(employee_name)
            return True
        else:
            return False

    def removeEmployee(self, employee_name):
        if employee_name in self.employees:
            self.employees.remove(employee_name)
            return True
        else:
            return False

    def getEmployees(self):
        return self.employees


class Company:
    def __init__(self):
        self.offices = []

    def openOffice(self, office_name):
        office_number = len(self.offices) + 1 
        office = Office(office_number, office_name)
        self.offices.append(office)
        return office

    def getOffice(self, office_number):
        for office in self.offices:
            if office.office_number == office_number:
                return office
        return None

    def addEmployee(self, employee_name, office_number):
        office = self.getOffice(office_number)
        if office:
            return office.addEmployee(employee_name)
        else:
            return False

    def removeEmployee(self, employee_name, office_number):
        office = self.getOffice(office_number)
        if office:
            return office.removeEmployee(employee_name)
        else:
            return False

    def transferEmployee(self, employee_name, old_office_number, new_office_number):
        old_office = self.getOffice(old_office_number)
        new_office = self.getOffice(new_office_number)

        if old_office and new_office:
            if employee_name in old_office.employees and employee_name not in new_office.employees:
                old_office.removeEmployee(employee_name)
                new_office.addEmployee(employee_name)
                return True
            else:
                return False
        else:
            return False

    def getEmployees(self, office_number):
        office = self.getOffice(office_number)
        if office:
            return office.getEmployees()
        else:
            return None



company = Company()
office1 = company.openOffice("Main Office")
office2 = company.openOffice("Branch Office")

company.addEmployee("John Doe", office1.office_number)
company.addEmployee("Jane Smith", office1.office_number)
company.addEmployee("Bob Johnson", office2.office_number)

print(company.getEmployees(office1.office_number))  
print(company.getEmployees(office2.office_number))  

company.transferEmployee("John Doe", office1.office_number, office2.office_number)

print(company.getEmployees(office1.office_number)) 
print(company.getEmployees(office2.office_number))  


