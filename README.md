# Java-DBMS-DS-Project




////    <<<<<   USER MANAGER CLASS  >>>>>>

import java.util.ArrayList;

public class UserManager {

    private final ArrayList<User> users = new ArrayList<>();
    private int nextUserId = 1001;

    public int generateUserId() {
        return nextUserId++;
    }

    public boolean addUser(User user) {

        if (user == null)
            return false;

        if (isUsernameExists(user.getUsername()))
            return false;

        if (user.getUserId() == 0)
            user.setUserId(generateUserId());

        users.add(user);
        return true;
    }


    public boolean isUsernameExists(String username) {

        for (User user : users) {

            if (user.getUsername().equalsIgnoreCase(username))
                return true;
        }

        return false;
    }

    public User searchById(int id) {

        for (User user : users) {

            if (user.getUserId() == id)
                return user;
        }

        return null;
    }

   

    public boolean deleteUser(int id) {

        User user = searchById(id);

        if (user == null)
            return false;

        users.remove(user);
        return true;
    }


    public int getTotalUsers() {
        return users.size();
    }

    public void displayAllUsers() {

        if (users.isEmpty()) {
            System.out.println("No users found.");
            return;
        }

        System.out.println("----------------------------------------------");

        for (User user : users) {
            System.out.println(user);
            System.out.println("----------------------------------------------");
        }
    }
}







////   <<<<<   USER CLASS   >>>>

import java.util.Scanner;

public class User {

    private int userId;
    private String name;
    private int age;
    private String gender;
    private String bloodGroup;
    private String phone;
    private String email;
    private String address;
    private String username;
    private String password;
    private String lastDonationDate;

    public User() {
    }

    public User(int userId, String name, int age, String gender, String bloodGroup, String phone, String email, String address, String username, String password, String lastDonationDate) {
        this.userId = userId;
        this.name = name;
        this.age = age;
        this.gender = gender;
        this.bloodGroup = bloodGroup;
        this.phone = phone;
        this.email = email;
        this.address = address;
        this.username = username;
        this.password = password;
        this.lastDonationDate = lastDonationDate;
    }

    public int getUserId() {
        return userId;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public String getGender() {
        return gender;
    }

    public String getBloodGroup() {
        return bloodGroup;
    }

    public String getPhone() {
        return phone;
    }

    public String getEmail() {
        return email;
    }

    public String getAddress() {
        return address;
    }

    public String getUsername() {
        return username;
    }

    public String getPassword() {
        return password;
    }

    public String getLastDonationDate() {
        return lastDonationDate;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public void setUserId(int userId) {
        this.userId = userId;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    public void setBloodGroup(String bloodGroup) {
        this.bloodGroup = bloodGroup;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public void setLastDonationDate(String lastDonationDate) {
        this.lastDonationDate = lastDonationDate;
    }

    public void viewProfile(User user) {
        System.out.println();
        System.out.println();
        System.out.println("            MY PROFILE");
        System.out.println();
        System.out.println();
        System.out.println("User ID            : " + user.getUserId());
        System.out.println("Full Name          : " + user.getName());
        System.out.println("Age                : " + user.getAge());
        System.out.println("Gender             : " + user.getGender());
        System.out.println("Blood Group        : " + user.getBloodGroup());
        System.out.println("Phone Number       : " + user.getPhone());
        System.out.println("Email              : " + user.getEmail());
        System.out.println("Address            : " + user.getAddress());
        System.out.println("Username           : " + user.getUsername());
        System.out.println("Last Donation Date : " + user.getLastDonationDate());

        System.out.println("========================================");
    }

    @Override
    public String toString() {
        return "User{" +
                "userId=" + userId +
                ", name='" + name + '\'' +
                ", age=" + age +
                ", gender='" + gender + '\'' +
                ", bloodGroup='" + bloodGroup + '\'' +
                ", phone='" + phone + '\'' +
                ", email='" + email + '\'' +
                ", address='" + address + '\'' +
                ", username='" + username + '\'' +
                ", lastDonationDate='" + lastDonationDate + '\'' +
                '}';
    }


}


//Admin Class
class Admin{
    int adminId;
    String adminName;
    String userName;
    String password;
    String email;
    String phoneNo;

    public Admin(int adminId, String adminName, String userName, String password, String email, String phoneNo) {
        this.adminId = adminId;
        this.adminName = adminName;
        this.userName = userName;
        this.password = password;
        this.email = email;
        this.phoneNo = phoneNo;
    }

    public int getAdminId() {
        return adminId;
    }
    public String getAdminName() {
        return adminName;
    }
    public String getUserName() {
        return userName;
    }
    public String getPassword() {
        return password;
    }
    public String getEmail() {
        return email;
    }
    public String getPhoneNo() {
        return phoneNo;
    }

    public void setAdminId(int adminId) {
        this.adminId = adminId;
    }
    public void setAdminName(String adminName) {
        this.adminName = adminName;
    }
    public void setUserName(String userName) {
        this.userName = userName;
    }
    public void setPassword(String password) {
        this.password = password;
    }
    public void setEmail(String email) {
        this.email = email;
    }
    public void setPhoneNo(String phoneNo) {
        this.phoneNo = phoneNo;
    }

    @Override
    public String toString() {
        return "Admin{" +
                "adminId=" + adminId +
                ", adminName='" + adminName + '\'' +
                ", userName='" + userName + '\'' +
                ", email='" + email + '\'' +
                ", phoneNo='" + phoneNo + '\'' +
                '}';
    }
}




//Donor Class
class Donor{
    int donorID;
    String donorName;
    int donorAge;
    String donorGender;
    String bloodGroup;
    String cityName;
    String phoneNo;
    String email;
    String donorHistory;
    Boolean available;

    public Donor(int donorID, String donorName, int donorAge, String donorGender, String bloodGroup, String cityName, String phoneNo, String email, String donorHistory, Boolean available) {
        this.donorID = donorID;
        this.donorName = donorName;
        this.donorAge = donorAge;
        this.donorGender = donorGender;
        this.bloodGroup = bloodGroup;
        this.cityName = cityName;
        this.phoneNo = phoneNo;
        this.email = email;
        this.donorHistory = donorHistory;
        this.available = available;
    }

    public int getDonorID() {
        return donorID;
    }
    public String getDonorName() {
        return donorName;
    }
    public int getDonorAge() {
        return donorAge;
    }
    public String getDonorGender() {
        return donorGender;
    }
    public String getBloodGroup() {
        return bloodGroup;
    }
    public String getCityName() {
        return cityName;
    }
    public String getPhoneNo() {
        return phoneNo;
    }
    public String getEmail() {
        return email;
    }
    public String getDonorHistory() {
        return donorHistory;
    }
    public Boolean getAvailable() {
        return available;
    }

    public void setDonorID(int donorID) {
        this.donorID = donorID;
    }
    public void setDonorName(String donorName) {
        this.donorName = donorName;
    }
    public void setDonorAge(int donorAge) {
        this.donorAge = donorAge;
    }
    public void setDonorGender(String donorGender) {
        this.donorGender = donorGender;
    }
    public void setBloodGroup(String bloodGroup) {
        this.bloodGroup = bloodGroup;
    }
    public void setCityName(String cityName) {
        this.cityName = cityName;
    }
    public void setPhoneNo(String phoneNo) {
        this.phoneNo = phoneNo;
    }
    public void setEmail(String email) {
        this.email = email;
    }
    public void setDonorHistory(String donorHistory) {
        this.donorHistory = donorHistory;
    }
    public void setAvailable(Boolean available) {
        this.available = available;
    }

    @Override
    public String toString() {
        return "Donor{" +
                "donorID=" + donorID +
                ", donorName='" + donorName + '\'' +
                ", donorAge=" + donorAge +
                ", donorGender='" + donorGender + '\'' +
                ", bloodGroup='" + bloodGroup + '\'' +
                ", cityName='" + cityName + '\'' +
                ", phoneNo='" + phoneNo + '\'' +
                ", email='" + email + '\'' +
                ", donorHistory='" + donorHistory + '\'' +
                ", available='" + available + '\'' +
                '}';
    }
}


//Blood Inventory Class
class BloodInventory{
    int inventoryId;
    String bloodGroup;
    int unitsAvailable;
    int minUnitsAvailability;

    public int getInventoryId() {
        return inventoryId;
    }
    public String getBloodGroup() {
        return bloodGroup;
    }
    public int getUnitsAvailable() {
        return unitsAvailable;
    }
    public int getMinUnitsAvailability() {
        return minUnitsAvailability;
    }

    public void setInventoryId(int inventoryId) {
        this.inventoryId = inventoryId;
    }
    public void setBloodGroup(String bloodGroup) {
        this.bloodGroup = bloodGroup;
    }
    public void setUnitsAvailable(int unitsAvailable) {
        this.unitsAvailable = unitsAvailable;
    }
    public void setMinUnitsAvailability(int minUnitsAvailability) {
        this.minUnitsAvailability = minUnitsAvailability;
    }

    @Override
    public String toString() {
        return "BloodInventory{" +
                "inventoryId=" + inventoryId +
                ", bloodGroup='" + bloodGroup + '\'' +
                ", unitsAvailable=" + unitsAvailable +
                ", minUnitsAvailability=" + minUnitsAvailability +
                '}';
        }
    }


    //Blood request
    class BloodRequest{
    int requestID;
    String patientName;
    int patientAge;
    String bloodGroup;
    int unitsRequired;
    String hospitalName;
    String cityName;
    String contactNo;
    String requestStatus;

    public BloodRequest(int requestID, String patientName, int patientAge, String bloodGroup, int unitsRequired, String hospitalName, String cityName, String contactNo, String requestStatus) {
        this.requestID = requestID;
        this.patientName = patientName;
        this.patientAge = patientAge;
        this.bloodGroup = bloodGroup;
        this.unitsRequired = unitsRequired;
        this.hospitalName = hospitalName;
        this.cityName = cityName;
        this.contactNo = contactNo;
        this.requestStatus = requestStatus;
    }

    public int getRequestID() {
        return requestID;
    }
    public String getPatientName() {
        return patientName;
    }
    public int getPatientAge() {
        return patientAge;
    }
    public String getBloodGroup() {
        return bloodGroup;
    }
    public int getUnitsRequired() {
        return unitsRequired;
    }
    public String getHospitalName() {
        return hospitalName;
    }
    public String getCityName() {
        return cityName;
    }
    public String getContactNo() {
        return contactNo;
    }
    public String getRequestStatus() {
        return requestStatus;
    }

    public void setRequestID(int requestID) {
        this.requestID = requestID;
    }
    public void setPatientName(String patientName) {
        this.patientName = patientName;
    }
    public void setPatientAge(int patientAge) {
        this.patientAge = patientAge;
    }
    public void setBloodGroup(String bloodGroup) {
        this.bloodGroup = bloodGroup;
    }
    public void setUnitsRequired(int unitsRequired) {
        this.unitsRequired = unitsRequired;
    }
    public void setHospitalName(String hospitalName) {
        this.hospitalName = hospitalName;
    }
    public void setCityName(String cityName) {
        this.cityName = cityName;
    }
    public void setContactNo(String contactNo) {
        this.contactNo = contactNo;
    }
    public void setRequestStatus(String requestStatus) {
        this.requestStatus = requestStatus;
    }

    @Override
    public String toString() {
        return "BloodRequest{" +
                "requestID=" + requestID +
                ", patientName='" + patientName + '\'' +
                ", patientAge=" + patientAge +
                ", bloodGroup='" + bloodGroup + '\'' +
                ", unitsRequired=" + unitsRequired +
                ", hospitalName='" + hospitalName + '\'' +
                ", cityName='" + cityName + '\'' +
                ", contactNo='" + contactNo + '\'' +
                ", requestStatus='" + requestStatus + '\'' +
                '}';
    }
}

// <<<<BLOOD REQUEST SERVICE CLASS>>>>


//this class provides services for managing BloodRequest class
import java.util.ArrayList;
import java.util.Scanner;

public class BloodRequestService {
    private final ArrayList<BloodRequest> requests=new ArrayList<>();
    private Scanner sc=new Scanner(System.in);
    private int nextRequestId=1;
    public BloodRequestService()
    {}

    public boolean addRequest(BloodRequest request)
    {
        if(request==null) {
            return false;
        }
            request.setRequestID(nextRequestId);
            nextRequestId++;
            request.setRequestStatus("Pending");
            requests.add(request);
        return true;
    }

    public BloodRequest searchRequest(int requestID)
    {
      for(BloodRequest request:requests)
      {
          if(request.getRequestID()==requestID)
          {
              return request;
          }
      }
      return null;
    }

    public boolean deleteRequest(int requestID)
    {
        BloodRequest request=searchRequest(requestID);
        if(request!=null)
        {
           requests.remove(request);
           System.out.println("Request deleted successfully.");
           return true;
        }
        System.out.println("No matching requests found.");
        return false;
    }

    public void updateRequest()
    {
        System.out.println("Enter the Request ID you want to update:");
        int requestID = sc.nextInt();
        sc.nextLine();

        BloodRequest request = searchRequest(requestID);

        if(request == null)
        {
            System.out.println("No matching request found.");
            return;
        }

        int choice;

        do
        {
            System.out.println("\n===== Update Request Menu =====");
            System.out.println("1. Update Patient Name");
            System.out.println("2. Update Patient Age");
            System.out.println("3. Update Blood Group");
            System.out.println("4. Update Units Required");
            System.out.println("5. Update Hospital Name");
            System.out.println("6. Update City");
            System.out.println("7. Update Contact Number");
            System.out.println("8. Update Priority");
            System.out.println("9. Exit");
            System.out.print("Enter your choice: ");

            choice = sc.nextInt();
            sc.nextLine();

            switch(choice)
            {
                case 1:
                    System.out.print("Enter Updated Patient Name: ");
                    String patientName = sc.nextLine();
                    while(patientName.trim().isEmpty())
                    {
                        System.out.print("Name cannot be empty. Enter again: ");
                        patientName = sc.nextLine();
                    }

                    request.setPatientName(patientName);
                    System.out.println("Patient name updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 2:
                    System.out.print("Enter Updated Patient Age: ");
                    int patientAge = sc.nextInt();

                    while(patientAge < 1 || patientAge > 110)
                    {
                        System.out.print("Invalid age! Please enter age between 1 and 110: ");
                        patientAge = sc.nextInt();
                    }
                    request.setPatientAge(patientAge);
                    sc.nextLine();
                    System.out.println("Patient age updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 3:
                    System.out.print("Enter Updated Blood Group: ");
                    String bloodGroup = sc.nextLine();
                    while(!(bloodGroup.equalsIgnoreCase("A+") ||
                            bloodGroup.equalsIgnoreCase("A-") ||
                            bloodGroup.equalsIgnoreCase("B+") ||
                            bloodGroup.equalsIgnoreCase("B-") ||
                            bloodGroup.equalsIgnoreCase("AB+") ||
                            bloodGroup.equalsIgnoreCase("AB-") ||
                            bloodGroup.equalsIgnoreCase("O+") ||
                            bloodGroup.equalsIgnoreCase("O-")))
                    {
                        System.out.print("Invalid Blood Group! Enter again: ");
                        bloodGroup = sc.nextLine();
                    }

                    request.setBloodGroup(bloodGroup.toUpperCase());
                    System.out.println("Blood group updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 4:
                    System.out.print("Enter Updated Units Required: ");
                    int units = sc.nextInt();

                    while(units < 1 || units > 10)
                    {
                        System.out.print("Units should be between 1 and 10: ");
                        units = sc.nextInt();
                    }

                    request.setUnitsRequired(units);
                    sc.nextLine();
                    System.out.println("Units updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 5:
                    System.out.print("Enter Updated Hospital Name: ");
                    String hospital = sc.nextLine();
                    while(hospital.trim().isEmpty())
                    {
                        System.out.print("Hospital name cannot be empty. Enter again: ");
                        hospital = sc.nextLine();
                    }

                    request.setHospitalName(hospital);
                    System.out.println("Hospital name updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 6:
                    System.out.print("Enter Updated City: ");
                    String city = sc.nextLine();
                    while(city.trim().isEmpty())
                    {
                        System.out.print("City name cannot be empty. Enter again: ");
                        city = sc.nextLine();
                    }

                    request.setCityName(city);
                    System.out.println("City updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 7:
                    System.out.print("Enter Updated Contact Number: ");
                    String contact = sc.nextLine();

                    while(contact.length()!=10 ||
                            !Character.isDigit(contact.charAt(0)) ||
                            !Character.isDigit(contact.charAt(1)) ||
                            !Character.isDigit(contact.charAt(2)) ||
                            !Character.isDigit(contact.charAt(3)) ||
                            !Character.isDigit(contact.charAt(4)) ||
                            !Character.isDigit(contact.charAt(5)) ||
                            !Character.isDigit(contact.charAt(6)) ||
                            !Character.isDigit(contact.charAt(7)) ||
                            !Character.isDigit(contact.charAt(8)) ||
                            !Character.isDigit(contact.charAt(9)))
                    {
                        System.out.print("Invalid Contact Number! Enter again: ");
                        contact = sc.nextLine();
                    }
                    request.setContactNo(contact);
                    System.out.println("Contact number updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 8:
                    System.out.print("Enter Updated Priority (High/Medium/Low): ");
                    String priority = sc.nextLine();
                    while(!(priority.equalsIgnoreCase("High") ||
                            priority.equalsIgnoreCase("Medium") ||
                            priority.equalsIgnoreCase("Low")))
                    {
                        System.out.print("Invalid Priority! Enter High, Medium or Low: ");
                        priority = sc.nextLine();
                    }

                    request.setPriority(priority);
                    System.out.println("Priority updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 9:
                    System.out.println("Exiting Update Menu...");
                    break;

                default:
                    System.out.println("Invalid choice.");
            }

        } while(choice != 9);
    }

    public void displayAllRequests()
    {
            if(requests.isEmpty())
            {
                System.out.println("No requests available.");
                return;
            }
        for(BloodRequest request:requests)
        {
            System.out.println(request);
        }
    }

    public void displayPendingRequests()
    {
        boolean found=false;
        for(BloodRequest request:requests)
        {
            if("Pending".equals(request.getRequestStatus())) //no null pointer exception
            {
                System.out.println(request);
                found=true;
            }
        }
        if(!found)
        {
            System.out.println("No pending requests.");
        }
    }

    public void displayCompletedRequests()
    {
        boolean found=false;
        for(BloodRequest request:requests)
        {
            if("Completed".equals(request.getRequestStatus()))
            {
                System.out.println(request);
                found=true;
            }
        }
        if(!found)
        {
            System.out.println("No completed requests.");
        }
    }

    public boolean cancelRequest(int requestID)
    {
        BloodRequest request = searchRequest(requestID);
        if(request!=null)
        {
            request.setRequestStatus("Cancelled");
            System.out.println("Request cancelled successfully.");
            return true;
        }
        else{
            System.out.println("No matching requests found.");
            return false;
        }
    }

    public boolean completeRequest(int requestID) {
        BloodRequest request = searchRequest(requestID);
        if (request != null) {
            request.setRequestStatus("Completed");
            System.out.println("Request completed successfully.");
            return true;
        } else {
            System.out.println("No matching request found.");
            return false;
        }
    }

    public void displayCriticalRequests() {
        boolean found = false;
        for (BloodRequest request : requests) {
            if ("High".equals(request.getPriority())) {
                System.out.println(request);
                found = true;
            }
        }
        if (!found) {
            System.out.println("No high priority requests.");
        }
    }

    public boolean assignDonor(int requestID, int donorID, String donorName) {
        BloodRequest request = searchRequest(requestID);
        if (request == null) {
            System.out.println("No matching requests found.");
            return false;
        } else if ("Cancelled".equals(request.getRequestStatus())||"Completed".equals(request.getRequestStatus())){
            System.out.println("Cannot assign donor. Request is already cancelled or completed.");
            return false;
        } else {
            request.setDonorID(donorID);
            request.setDonorName(donorName);
            request.setRequestStatus("Assigned");
            System.out.println("Donor assigned successfully.");
            return true;
        }
    }
}


//<<<<<<DonationHistory class>>>>



//this class only stores donation history details..
public class DonationHistory {
    private int requestID;
    private int historyID;
    private int donorID;
    private String donorName;
    private String patientName;
    private String bloodGroup;
    private int unitsDonated;
    private String hospitalName;
    private String cityName;
    private String donationDate;

    public DonationHistory(){}

    public DonationHistory(int requestID,int historyID, int donorID, String donorName,
                           String patientName, String bloodGroup, int unitsDonated, String hospitalName,
                           String cityName, String donationDate) {
        this.requestID=requestID;
        this.historyID = historyID;
        this.donorID = donorID;
        this.donorName = donorName;
        this.patientName = patientName;
        this.bloodGroup = bloodGroup;
        this.unitsDonated = unitsDonated;
        this.hospitalName = hospitalName;
        this.cityName = cityName;
        this.donationDate = donationDate;
    }

//getters
    public int getRequestID() {
        return requestID;
    }
    public int getHistoryID() {
        return historyID;
    }
    public int getDonorID() {
        return donorID;
    }
    public String getDonorName() {
        return donorName;
    }
    public String getPatientName() {
        return patientName;
    }
    public String getBloodGroup() {
        return bloodGroup;
    }
    public int getUnitsDonated() {
        return unitsDonated;
    }
    public String getHospitalName() {
        return hospitalName;
    }
    public String getCityName() {
        return cityName;
    }
    public String getDonationDate() {
        return donationDate;
    }

 //setters
    public void setRequestID(int requestID) {
        this.requestID = requestID;
    }
    public void setHistoryID(int historyID) {
        this.historyID = historyID;
    }
    public void setDonorID(int donorID) {
        this.donorID = donorID;
    }
    public void setDonorName(String donorName) {
        this.donorName = donorName;
    }
    public void setPatientName(String patientName) {
        this.patientName = patientName;
    }
    public void setBloodGroup(String bloodGroup) {
        this.bloodGroup = bloodGroup;
    }
    public void setUnitsDonated(int unitsDonated) {
        this.unitsDonated = unitsDonated;
    }
    public void setHospitalName(String hospitalName) {
        this.hospitalName = hospitalName;
    }
    public void setCityName(String cityName) {
        this.cityName = cityName;
    }
    public void setDonationDate(String donationDate) {
        this.donationDate = donationDate;
    }

    @Override
    public String toString() {
        return "DonationHistory{" +
                "requestID=" + requestID +
                ", historyID=" + historyID +
                ", donorID=" + donorID +
                ", donorName='" + donorName + '\'' +
                ", patientName='" + patientName + '\'' +
                ", bloodGroup='" + bloodGroup + '\'' +
                ", unitsDonated=" + unitsDonated +
                ", hospitalName='" + hospitalName + '\'' +
                ", cityName='" + cityName + '\'' +
                ", donationDate='" + donationDate + '\'' +
                '}';
    }
}





































































///  AARYA'S CODE

class Admin {
    int adminId;
    String adminName;
    String userName;
    String password;
    String email;
    String phoneNo;

    public Admin(int adminId, String adminName, String userName, String password, String email, String phoneNo) {
        this.adminId = adminId;
        this.adminName = adminName;
        this.userName = userName;
        this.password = password;
        this.email = email;
        this.phoneNo = phoneNo;
    }

    public int getAdminId() {
        return adminId;
    }

    public String getAdminName() {
        return adminName;
    }

    public String getUserName() {
        return userName;
    }

    public String getPassword() {
        return password;
    }

    public String getEmail() {
        return email;
    }

    public String getPhoneNo() {
        return phoneNo;
    }

    public void setAdminId(int adminId) {
        this.adminId = adminId;
    }

    public void setAdminName(String adminName) {
        this.adminName = adminName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public void setPhoneNo(String phoneNo) {
        this.phoneNo = phoneNo;
    }

    @Override
    public String toString() {
        return "Admin{" +
                "adminId=" + adminId +
                ", adminName='" + adminName + '\'' +
                ", userName='" + userName + '\'' +
                ", email='" + email + '\'' +
                ", phoneNo='" + phoneNo + '\'' +
                '}';
    }
}


public class BloodInventory {

    private int inventoryId;
    private String bloodGroup;
    private int unitsAvailable;
    private int minUnitsAvailability;

    public BloodInventory() {
    }

    public BloodInventory(int inventoryId, String bloodGroup,
                          int unitsAvailable, int minUnitsAvailability) {
        this.inventoryId = inventoryId;
        this.bloodGroup = bloodGroup;
        this.unitsAvailable = unitsAvailable;
        this.minUnitsAvailability = minUnitsAvailability;
    }

    public int getInventoryId() {
        return inventoryId;
    }

    public String getBloodGroup() {
        return bloodGroup;
    }

    public int getUnitsAvailable() {
        return unitsAvailable;
    }

    public int getMinUnitsAvailability() {
        return minUnitsAvailability;
    }

    public void setInventoryId(int inventoryId) {
        this.inventoryId = inventoryId;
    }

    public void setBloodGroup(String bloodGroup) {
        this.bloodGroup = bloodGroup;
    }

    public void setUnitsAvailable(int unitsAvailable) {
        this.unitsAvailable = unitsAvailable;
    }

    public void setMinUnitsAvailability(int minUnitsAvailability) {
        this.minUnitsAvailability = minUnitsAvailability;
    }

    @Override
    public String toString() {
        return "BloodInventory{" +
                "inventoryId=" + inventoryId +
                ", bloodGroup='" + bloodGroup + '\'' +
                ", unitsAvailable=" + unitsAvailable +
                ", minUnitsAvailability=" + minUnitsAvailability +
                '}';
    }
}


//Blood request
public class BloodRequest {
    int requestID;
    String patientName;
    int patientAge;
    String bloodGroup;
    int unitsRequired;
    String hospitalName;
    String cityName;
    String contactNo;
    String requestStatus;
    String donorName;
    String priority;
    int donorID;

    public BloodRequest(int requestID, String patientName, int patientAge, String bloodGroup, int unitsRequired, String hospitalName, String cityName, String contactNo, String requestStatus) {
        this.requestID = requestID;
        this.patientName = patientName;
        this.patientAge = patientAge;
        this.bloodGroup = bloodGroup;
        this.unitsRequired = unitsRequired;
        this.hospitalName = hospitalName;
        this.cityName = cityName;
        this.contactNo = contactNo;
        this.requestStatus = requestStatus;
    }

    public void getPrioritry(){ }

    public int getRequestID() {
        return requestID;
    }

    public String getPatientName() {
        return patientName;
    }

    public int getPatientAge() {
        return patientAge;
    }

    public String getBloodGroup() {
        return bloodGroup;
    }

    public int getUnitsRequired() {
        return unitsRequired;
    }

    public String getHospitalName() {
        return hospitalName;
    }

    public String getCityName() {
        return cityName;
    }

    public String getContactNo() {
        return contactNo;
    }

    public String getPriority() {return priority; }

    public String getDonorName() {return donorName; }

    public String getRequestStatus() {
        return requestStatus;
    }

    public void setRequestID(int requestID) {
        this.requestID = requestID;
    }

    public void setPatientName(String patientName) {
        this.patientName = patientName;
    }

    public void setPatientAge(int patientAge) {
        this.patientAge = patientAge;
    }

    public void setBloodGroup(String bloodGroup) {
        this.bloodGroup = bloodGroup;
    }

    public void setUnitsRequired(int unitsRequired) {
        this.unitsRequired = unitsRequired;
    }

    public void setHospitalName(String hospitalName) {
        this.hospitalName = hospitalName;
    }

    public void setCityName(String cityName) {
        this.cityName = cityName;
    }

    public void setContactNo(String contactNo) {
        this.contactNo = contactNo;
    }

    public void setRequestStatus(String requestStatus) {
        this.requestStatus = requestStatus;
    }

    public void setDonorName(String donorName){this.donorName = donorName; }

    public void setPriority(String priority) {this.priority = priority; }
    @Override
    public String toString() {
        return "BloodRequest{" +
                "requestID=" + requestID +
                ", patientName='" + patientName + '\'' +
                ", patientAge=" + patientAge +
                ", bloodGroup='" + bloodGroup + '\'' +
                ", unitsRequired=" + unitsRequired +
                ", hospitalName='" + hospitalName + '\'' +
                ", cityName='" + cityName + '\'' +
                ", contactNo='" + contactNo + '\'' +
                ", requestStatus='" + requestStatus + '\'' +
                '}';
    }

    public void setDonorID(int donorID) {
        this.donorID = donorID;
    }
}



// <<<>>>

//this class provides services for managing BloodRequest class import java.util.ArrayList; import java.util.Scanner;

import java.util.ArrayList;
import java.util.Scanner;

public class BloodRequestService {

    private final ArrayList<BloodRequest> requests = new ArrayList<>();

    private Scanner sc=new Scanner(System.in);

    private int nextRequestId=1;

    public BloodRequestService() {}

    public boolean addRequest(BloodRequest request)
    {
        if(request==null) {
            return false;
        }
        request.setRequestID(nextRequestId);
        nextRequestId++;
        request.setRequestStatus("Pending");
        requests.add(request);
        return true;
    }

    public BloodRequest searchRequest(int requestID)
    {
        for(BloodRequest request : requests)
        {
            if(request.getRequestID()==requestID)
            {
                return request;
            }
        }
        return null;
    }

    public boolean deleteRequest(int requestID)
    {
        BloodRequest request=searchRequest(requestID);
        if(request!=null)
        {
            requests.remove(request);
            System.out.println("Request deleted successfully.");
            return true;
        }
        System.out.println("No matching requests found.");
        return false;
    }

    public void updateRequest()
    {
        System.out.println("Enter the Request ID you want to update:");
        int requestID = sc.nextInt();
        sc.nextLine();

        BloodRequest request = searchRequest(requestID);

        if(request == null)
        {
            System.out.println("No matching request found.");
            return;
        }

        int choice;

        do
        {
            System.out.println("\n===== Update Request Menu =====");
            System.out.println("1. Update Patient Name");
            System.out.println("2. Update Patient Age");
            System.out.println("3. Update Blood Group");
            System.out.println("4. Update Units Required");
            System.out.println("5. Update Hospital Name");
            System.out.println("6. Update City");
            System.out.println("7. Update Contact Number");
            System.out.println("8. Update Priority");
            System.out.println("9. Exit");
            System.out.print("Enter your choice: ");

            choice = sc.nextInt();
            sc.nextLine();

            switch(choice)
            {
                case 1:
                    System.out.print("Enter Updated Patient Name: ");
                    String patientName = sc.nextLine();
                    while(patientName.trim().isEmpty())
                    {
                        System.out.print("Name cannot be empty. Enter again: ");
                        patientName = sc.nextLine();
                    }

                    request.setPatientName(patientName);
                    System.out.println("Patient name updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 2:
                    System.out.print("Enter Updated Patient Age: ");
                    int patientAge = sc.nextInt();

                    while(patientAge < 1 || patientAge > 110)
                    {
                        System.out.print("Invalid age! Please enter age between 1 and 110: ");
                        patientAge = sc.nextInt();
                    }
                    request.setPatientAge(patientAge);
                    sc.nextLine();
                    System.out.println("Patient age updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 3:
                    System.out.print("Enter Updated Blood Group: ");
                    String bloodGroup = sc.nextLine();
                    while(!(bloodGroup.equalsIgnoreCase("A+") ||
                            bloodGroup.equalsIgnoreCase("A-") ||
                            bloodGroup.equalsIgnoreCase("B+") ||
                            bloodGroup.equalsIgnoreCase("B-") ||
                            bloodGroup.equalsIgnoreCase("AB+") ||
                            bloodGroup.equalsIgnoreCase("AB-") ||
                            bloodGroup.equalsIgnoreCase("O+") ||
                            bloodGroup.equalsIgnoreCase("O-")))
                    {
                        System.out.print("Invalid Blood Group! Enter again: ");
                        bloodGroup = sc.nextLine();
                    }

                    request.setBloodGroup(bloodGroup.toUpperCase());
                    System.out.println("Blood group updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 4:
                    System.out.print("Enter Updated Units Required: ");
                    int units = sc.nextInt();

                    while(units < 1 || units > 10)
                    {
                        System.out.print("Units should be between 1 and 10: ");
                        units = sc.nextInt();
                    }

                    request.setUnitsRequired(units);
                    sc.nextLine();
                    System.out.println("Units updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 5:
                    System.out.print("Enter Updated Hospital Name: ");
                    String hospital = sc.nextLine();
                    while(hospital.trim().isEmpty())
                    {
                        System.out.print("Hospital name cannot be empty. Enter again: ");
                        hospital = sc.nextLine();
                    }

                    request.setHospitalName(hospital);
                    System.out.println("Hospital name updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 6:
                    System.out.print("Enter Updated City: ");
                    String city = sc.nextLine();
                    while(city.trim().isEmpty())
                    {
                        System.out.print("City name cannot be empty. Enter again: ");
                        city = sc.nextLine();
                    }

                    request.setCityName(city);
                    System.out.println("City updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 7:
                    System.out.print("Enter Updated Contact Number: ");
                    String contact = sc.nextLine();

                    while(contact.length()!=10 ||
                            !Character.isDigit(contact.charAt(0)) ||
                            !Character.isDigit(contact.charAt(1)) ||
                            !Character.isDigit(contact.charAt(2)) ||
                            !Character.isDigit(contact.charAt(3)) ||
                            !Character.isDigit(contact.charAt(4)) ||
                            !Character.isDigit(contact.charAt(5)) ||
                            !Character.isDigit(contact.charAt(6)) ||
                            !Character.isDigit(contact.charAt(7)) ||
                            !Character.isDigit(contact.charAt(8)) ||
                            !Character.isDigit(contact.charAt(9)))
                    {
                        System.out.print("Invalid Contact Number! Enter again: ");
                        contact = sc.nextLine();
                    }
                    request.setContactNo(contact);
                    System.out.println("Contact number updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 8:
                    System.out.print("Enter Updated Priority (High/Medium/Low): ");
                    String priority = sc.nextLine();
                    while(!(priority.equalsIgnoreCase("High") ||
                            priority.equalsIgnoreCase("Medium") ||
                            priority.equalsIgnoreCase("Low")))
                    {
                        System.out.print("Invalid Priority! Enter High, Medium or Low: ");
                        priority = sc.nextLine();
                    }

                    request.setPriority(priority);
                    System.out.println("Priority updated successfully.");
                    // JDBC Connectivity...
                    break;

                case 9:
                    System.out.println("Exiting Update Menu...");
                    break;

                default:
                    System.out.println("Invalid choice.");
            }

        } while(choice != 9);
    }

    public void displayAllRequests()
    {
        if(requests.isEmpty())
        {
            System.out.println("No requests available.");
            return;
        }
        for(BloodRequest request:requests)
        {
            System.out.println(request);
        }
    }

    public void displayPendingRequests()
    {
        boolean found=false;
        for(BloodRequest request:requests)
        {
            if("Pending".equals(request.getRequestStatus())) //no null pointer exception
            {
                System.out.println(request);
                found=true;
            }
        }
        if(!found)
        {
            System.out.println("No pending requests.");
        }
    }

    public void displayCompletedRequests()
    {
        boolean found=false;
        for(BloodRequest request:requests)
        {
            if("Completed".equals(request.getRequestStatus()))
            {
                System.out.println(request);
                found=true;
            }
        }
        if(!found)
        {
            System.out.println("No completed requests.");
        }
    }

    public boolean cancelRequest(int requestID)
    {
        BloodRequest request = searchRequest(requestID);
        if(request!=null)
        {
            request.setRequestStatus("Cancelled");
            System.out.println("Request cancelled successfully.");
            return true;
        }
        else{
            System.out.println("No matching requests found.");
            return false;
        }
    }

    public boolean completeRequest(int requestID) {
        BloodRequest request = searchRequest(requestID);
        if (request != null) {
            request.setRequestStatus("Completed");
            System.out.println("Request completed successfully.");
            return true;
        } else {
            System.out.println("No matching request found.");
            return false;
        }
    }

    public void displayCriticalRequests() {
        boolean found = false;
        for (BloodRequest request : requests) {
            if ("High".equals(request.getPriority())) {
                System.out.println(request);
                found = true;
            }
        }
        if (!found) {
            System.out.println("No high priority requests.");
        }
    }

    public boolean assignDonor(int requestID, int donorID, String donorName) {
        BloodRequest request = searchRequest(requestID);
        if (request == null) {
            System.out.println("No matching requests found.");
            return false;
        } else if ("Cancelled".equals(request.getRequestStatus())||"Completed".equals(request.getRequestStatus())){
            System.out.println("Cannot assign donor. Request is already cancelled or completed.");
            return false;
        } else {
            request.setDonorID(donorID);
            request.setDonorName(donorName);
            request.setRequestStatus("Assigned");
            System.out.println("Donor assigned successfully.");
            return true;
        }
    }
}

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DatabaseConnection {

    // PostgreSQL Database Details
    private static final String URL =
            "jdbc:mysql://localhost:3306/lifelink";

    private static final String USER =
            "root";

    private static final String PASSWORD =
            "";


    // ==========================================
    // GET DATABASE CONNECTION
    // ==========================================

    public static Connection getConnection() {

        try {

            Connection con =
                    DriverManager.getConnection(URL, USER, PASSWORD);

            return con;

        } catch (SQLException e) {

            System.out.println("Database connection failed!");
            System.out.println("Error: " + e.getMessage());

            return null;
        }
    }


    // ==========================================
    // CLOSE DATABASE CONNECTION
    // ==========================================

    public static void closeConnection(Connection con) {

        if (con != null) {

            try {

                con.close();

                System.out.println("Database connection closed.");

            } catch (SQLException e) {

                System.out.println(
                        "Error while closing connection: "
                                + e.getMessage()
                );
            }
        }
    }
}



//<<<<<>>>
//this class only stores donation history details..
public class DonationHistory {
    private int requestID;
    private int historyID;
    private int donorID;
    private String donorName;
    private String patientName;
    private String bloodGroup;
    private int unitsDonated;
    private String hospitalName;
    private String cityName;
    private String donationDate;

    public DonationHistory() {
    }

    public DonationHistory(int requestID, int historyID, int donorID, String donorName,
                           String patientName, String bloodGroup, int unitsDonated, String hospitalName,
                           String cityName, String donationDate) {
        this.requestID = requestID;
        this.historyID = historyID;
        this.donorID = donorID;
        this.donorName = donorName;
        this.patientName = patientName;
        this.bloodGroup = bloodGroup;
        this.unitsDonated = unitsDonated;
        this.hospitalName = hospitalName;
        this.cityName = cityName;
        this.donationDate = donationDate;
    }

    //getters
    public int getRequestID() {
        return requestID;
    }

    public int getHistoryID() {
        return historyID;
    }

    public int getDonorID() {
        return donorID;
    }

    public String getDonorName() {
        return donorName;
    }

    public String getPatientName() {
        return patientName;
    }

    public String getBloodGroup() {
        return bloodGroup;
    }

    public int getUnitsDonated() {
        return unitsDonated;
    }

    public String getHospitalName() {
        return hospitalName;
    }

    public String getCityName() {
        return cityName;
    }

    public String getDonationDate() {
        return donationDate;
    }

    //setters
    public void setRequestID(int requestID) {
        this.requestID = requestID;
    }

    public void setHistoryID(int historyID) {
        this.historyID = historyID;
    }

    public void setDonorID(int donorID) {
        this.donorID = donorID;
    }

    public void setDonorName(String donorName) {
        this.donorName = donorName;
    }

    public void setPatientName(String patientName) {
        this.patientName = patientName;
    }

    public void setBloodGroup(String bloodGroup) {
        this.bloodGroup = bloodGroup;
    }

    public void setUnitsDonated(int unitsDonated) {
        this.unitsDonated = unitsDonated;
    }

    public void setHospitalName(String hospitalName) {
        this.hospitalName = hospitalName;
    }

    public void setCityName(String cityName) {
        this.cityName = cityName;
    }

    public void setDonationDate(String donationDate) {
        this.donationDate = donationDate;
    }

    @Override
    public String toString() {
        return "DonationHistory{" +
                "requestID=" + requestID +
                ", historyID=" + historyID +
                ", donorID=" + donorID +
                ", donorName='" + donorName + '\'' +
                ", patientName='" + patientName + '\'' +
                ", bloodGroup='" + bloodGroup + '\'' +
                ", unitsDonated=" + unitsDonated +
                ", hospitalName='" + hospitalName + '\'' +
                ", cityName='" + cityName + '\'' +
                ", donationDate='" + donationDate + '\'' +
                '}';
    }
}

class Donor {
    int donorID;
    String donorName;
    int donorAge;
    String donorGender;
    String bloodGroup;
    String cityName;
    String phoneNo;
    String email;
    String donorHistory;
    Boolean available;

    public Donor(int donorID, String donorName, int donorAge, String donorGender, String bloodGroup, String cityName, String phoneNo, String email, String donorHistory, Boolean available) {
        this.donorID = donorID;
        this.donorName = donorName;
        this.donorAge = donorAge;
        this.donorGender = donorGender;
        this.bloodGroup = bloodGroup;
        this.cityName = cityName;
        this.phoneNo = phoneNo;
        this.email = email;
        this.donorHistory = donorHistory;
        this.available = available;
    }

    public int getDonorID() {
        return donorID;
    }

    public String getDonorName() {
        return donorName;
    }

    public int getDonorAge() {
        return donorAge;
    }

    public String getDonorGender() {
        return donorGender;
    }

    public String getBloodGroup() {
        return bloodGroup;
    }

    public String getCityName() {
        return cityName;
    }

    public String getPhoneNo() {
        return phoneNo;
    }

    public String getEmail() {
        return email;
    }

    public String getDonorHistory() {
        return donorHistory;
    }

    public Boolean getAvailable() {
        return available;
    }

    public void setDonorID(int donorID) {
        this.donorID = donorID;
    }

    public void setDonorName(String donorName) {
        this.donorName = donorName;
    }

    public void setDonorAge(int donorAge) {
        this.donorAge = donorAge;
    }

    public void setDonorGender(String donorGender) {
        this.donorGender = donorGender;
    }

    public void setBloodGroup(String bloodGroup) {
        this.bloodGroup = bloodGroup;
    }

    public void setCityName(String cityName) {
        this.cityName = cityName;
    }

    public void setPhoneNo(String phoneNo) {
        this.phoneNo = phoneNo;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public void setDonorHistory(String donorHistory) {
        this.donorHistory = donorHistory;
    }

    public void setAvailable(Boolean available) {
        this.available = available;
    }


    @Override
    public String toString() {
        return "Donor{" +
                "donorID=" + donorID +
                ", donorName='" + donorName + '\'' +
                ", donorAge=" + donorAge +
                ", donorGender='" + donorGender + '\'' +
                ", bloodGroup='" + bloodGroup + '\'' +
                ", cityName='" + cityName + '\'' +
                ", phoneNo='" + phoneNo + '\'' +
                ", email='" + email + '\'' +
                ", donorHistory='" + donorHistory + '\'' +
                ", available='" + available + '\'' +
                '}';
    }
}



import java.util.Scanner;

public class EditProfile {

    Scanner sc = new Scanner(System.in);

    public void editProfile(User user) {

        int choice;

        do {
            System.out.println("\n====================================");
            System.out.println("           EDIT PROFILE");
            System.out.println("====================================");
            System.out.println("1. Edit Name");
            System.out.println("2. Edit Phone Number");
            System.out.println("3. Edit Email");
            System.out.println("4. Edit Address");
            System.out.println("5. Edit Age");
            System.out.println("6. Edit Blood Group");
            System.out.println("7. Save Changes");
            System.out.println("8. Back");
            System.out.println("====================================");
            System.out.print("Enter Choice : ");

            while (true) {
                try {
                    choice = Integer.parseInt(sc.nextLine());

                    if (choice >= 1 && choice <= 8) {
                        break;
                    }

                    System.out.print("Enter a valid choice (1-8): ");

                } catch (NumberFormatException e) {
                    System.out.print("Invalid input! Enter numbers only: ");
                }
            }

            switch (choice) {

                case 1:
                    editName(user);
                    break;

                case 2:
                    editPhone(user);
                    break;

                case 3:
                    editEmail(user);
                    break;

                case 4:
                    editAddress(user);
                    break;

                case 5:
                    editAge(user);
                    break;

                case 6:
                    editBloodGroup(user);
                    break;

                case 7:
                    saveChanges(user);
                    break;

                case 8:
                    System.out.println("\nReturning to Profile...");
                    break;
            }

        } while (choice != 8);
    }


    // ================================
    // EDIT NAME
    // ================================

    public void editName(User user) {

        String name;

        while (true) {

            System.out.print("Enter New Name : ");
            name = sc.nextLine().trim();

            if (name.isEmpty()) {
                System.out.println("Name cannot be empty.");
                continue;
            }

            if (!name.matches("[a-zA-Z ]+")) {
                System.out.println("Name should contain letters and spaces only.");
                continue;
            }

            break;
        }

        user.setName(name);

        System.out.println("Name Updated Successfully.");
    }


    // ================================
    // EDIT PHONE
    // ================================

    public void editPhone(User user) {

        String phone;

        while (true) {

            System.out.print("Enter New Phone Number : ");
            phone = sc.nextLine().trim();

            if (!phone.matches("\\d{10}")) {
                System.out.println(
                        "Invalid phone number! Enter exactly 10 digits."
                );
                continue;
            }

            break;
        }

        user.setPhone(phone);

        System.out.println("Phone Number Updated Successfully.");
    }


    // ================================
    // EDIT EMAIL
    // ================================

    public void editEmail(User user) {

        String email;

        while (true) {

            System.out.print("Enter New Email : ");
            email = sc.nextLine().trim();

            if (email.isEmpty()) {
                System.out.println("Email cannot be empty.");
                continue;
            }

            if (!email.matches(
                    "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$")) {

                System.out.println("Invalid email format.");
                continue;
            }

            break;
        }

        user.setEmail(email);

        System.out.println("Email Updated Successfully.");
    }


    // ================================
    // EDIT ADDRESS
    // ================================

    public void editAddress(User user) {

        String address;

        while (true) {

            System.out.print("Enter New Address : ");
            address = sc.nextLine().trim();

            if (address.isEmpty()) {
                System.out.println("Address cannot be empty.");
                continue;
            }

            break;
        }

        user.setAddress(address);

        System.out.println("Address Updated Successfully.");
    }


    // ================================
    // EDIT AGE
    // ================================

    public void editAge(User user) {

        int age;

        while (true) {

            System.out.print("Enter New Age : ");

            try {

                age = Integer.parseInt(sc.nextLine());

                if (age < 1 || age > 120) {
                    System.out.println(
                            "Invalid age! Enter age between 1 and 120."
                    );
                    continue;
                }

                break;

            } catch (NumberFormatException e) {

                System.out.println("Invalid input! Enter numbers only.");
            }
        }

        user.setAge(age);

        System.out.println("Age Updated Successfully.");
    }


    // ================================
    // EDIT BLOOD GROUP
    // ================================

    public void editBloodGroup(User user) {

        String bloodGroup;

        while (true) {

            System.out.print("Enter New Blood Group : ");
            bloodGroup = sc.nextLine().trim().toUpperCase();

            if (!(bloodGroup.equals("A+") ||
                    bloodGroup.equals("A-") ||
                    bloodGroup.equals("B+") ||
                    bloodGroup.equals("B-") ||
                    bloodGroup.equals("AB+") ||
                    bloodGroup.equals("AB-") ||
                    bloodGroup.equals("O+") ||
                    bloodGroup.equals("O-"))) {

                System.out.println(
                        "Invalid Blood Group! " +
                                "Enter A+, A-, B+, B-, AB+, AB-, O+ or O-."
                );

                continue;
            }

            break;
        }

        user.setBloodGroup(bloodGroup);

        System.out.println("Blood Group Updated Successfully.");
    }


    // ================================
    // SAVE CHANGES
    // ================================

    public void saveChanges(User user) {

        System.out.println("\n====================================");
        System.out.println(" Profile Updated Successfully!");
        System.out.println(" Changes Saved.");
        System.out.println("====================================");

        // JDBC will be added later:
        // UserManager.updateUserInDB(user);
    }
}


import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Scanner;

public class FileManager {

    // Save Users
    public void saveUsers(ArrayList<User> users) {

        if (users == null || users.isEmpty()) {
            System.out.println("No user data available to save.");
            return;
        }

        try {
            FileWriter writer = new FileWriter("users.txt");

            for (User user : users) {
                if (user != null) {
                    writer.write(user.toString());
                    writer.write("\n");
                }
            }

            writer.close();

            System.out.println("User data saved successfully.");

        } catch (IOException e) {
            System.out.println("Error while saving user data.");
        }
    }


    // Save Donors
    public void saveDonors(ArrayList<Donor> donors) {

        if (donors == null || donors.isEmpty()) {
            System.out.println("No donor data available to save.");
            return;
        }

        try {
            FileWriter writer = new FileWriter("donors.txt");

            for (Donor donor : donors) {
                if (donor != null) {
                    writer.write(donor.toString());
                    writer.write("\n");
                }
            }

            writer.close();

            System.out.println("Donor data saved successfully.");

        } catch (IOException e) {
            System.out.println("Error while saving donor data.");
        }
    }


    // Save Blood Requests
    public void saveBloodRequests(ArrayList<BloodRequest> requests) {

        if (requests == null || requests.isEmpty()) {
            System.out.println("No blood request data available to save.");
            return;
        }

        try {
            FileWriter writer = new FileWriter("blood_requests.txt");

            for (BloodRequest request : requests) {
                if (request != null) {
                    writer.write(request.toString());
                    writer.write("\n");
                }
            }

            writer.close();

            System.out.println("Blood request data saved successfully.");

        } catch (IOException e) {
            System.out.println("Error while saving blood request data.");
        }
    }


    // Save Blood Inventory
    public void saveBloodInventory(ArrayList<BloodInventory> inventory) {

        if (inventory == null || inventory.isEmpty()) {
            System.out.println("No blood inventory data available to save.");
            return;
        }

        try {
            FileWriter writer = new FileWriter("blood_inventory.txt");

            for (BloodInventory item : inventory) {
                if (item != null) {
                    writer.write(item.toString());
                    writer.write("\n");
                }
            }

            writer.close();

            System.out.println("Blood inventory data saved successfully.");

        } catch (IOException e) {
            System.out.println("Error while saving blood inventory.");
        }
    }


    // Save Donation History
    public void saveDonationHistory(ArrayList<DonationHistory> history) {

        if (history == null || history.isEmpty()) {
            System.out.println("No donation history available to save.");
            return;
        }

        try {
            FileWriter writer = new FileWriter("donation_history.txt");

            for (DonationHistory donation : history) {
                if (donation != null) {
                    writer.write(donation.toString());
                    writer.write("\n");
                }
            }

            writer.close();

            System.out.println("Donation history saved successfully.");

        } catch (IOException e) {
            System.out.println("Error while saving donation history.");
        }
    }


    // Read File
    public void readFile(String fileName) {

        if (fileName == null || fileName.trim().isEmpty()) {
            System.out.println("Invalid file name.");
            return;
        }

        File file = new File(fileName);

        if (!file.exists()) {
            System.out.println("File does not exist.");
            return;
        }

        try {
            Scanner fileScanner = new Scanner(file);

            while (fileScanner.hasNextLine()) {
                System.out.println(fileScanner.nextLine());
            }

            fileScanner.close();

        } catch (IOException e) {
            System.out.println("Error while reading file.");
        }
    }


    // Save Report
    public void saveReport(String fileName, String report) {

        if (fileName == null || fileName.trim().isEmpty()) {
            System.out.println("Invalid file name.");
            return;
        }

        if (report == null || report.trim().isEmpty()) {
            System.out.println("Report cannot be empty.");
            return;
        }

        try {
            FileWriter writer = new FileWriter(fileName);

            writer.write(report);

            writer.close();

            System.out.println("Report saved successfully.");

        } catch (IOException e) {
            System.out.println("Error while saving report.");
        }
    }


    // Append Data to Existing File
    public void appendToFile(String fileName, String data) {

        if (fileName == null || fileName.trim().isEmpty()) {
            System.out.println("Invalid file name.");
            return;
        }

        if (data == null || data.trim().isEmpty()) {
            System.out.println("Data cannot be empty.");
            return;
        }

        try {
            FileWriter writer = new FileWriter(fileName, true);

            writer.write(data);
            writer.write("\n");

            writer.close();

            System.out.println("Data added to file successfully.");

        } catch (IOException e) {
            System.out.println("Error while appending data.");
        }
    }


    // Delete File
    public void deleteFile(String fileName) {

        if (fileName == null || fileName.trim().isEmpty()) {
            System.out.println("Invalid file name.");
            return;
        }

        File file = new File(fileName);

        if (!file.exists()) {
            System.out.println("File does not exist.");
            return;
        }

        if (file.delete()) {
            System.out.println("File deleted successfully.");
        } else {
            System.out.println("Unable to delete file.");
        }
    }
}

import java.util.Scanner;

public class User {

    private int userId;
    private String name;
    private int age;
    private String gender;
    private String bloodGroup;
    private String phone;
    private String email;
    private String address;
    private String username;
    private String password;
    private String lastDonationDate;

    public User() {
    }

    public User(int userId, String name, int age, String gender, String bloodGroup, String phone, String email, String address, String username, String password, String lastDonationDate) {
        this.userId = userId;
        this.name = name;
        this.age = age;
        this.gender = gender;
        this.bloodGroup = bloodGroup;
        this.phone = phone;
        this.email = email;
        this.address = address;
        this.username = username;
        this.password = password;
        this.lastDonationDate = lastDonationDate;
    }

    public int getUserId() {
        return userId;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public String getGender() {
        return gender;
    }

    public String getBloodGroup() {
        return bloodGroup;
    }

    public String getPhone() {
        return phone;
    }

    public String getEmail() {
        return email;
    }

    public String getAddress() {
        return address;
    }

    public String getUsername() {
        return username;
    }

    public String getPassword() {
        return password;
    }

    public String getLastDonationDate() {
        return lastDonationDate;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public void setUserId(int userId) {
        this.userId = userId;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }

    public void setBloodGroup(String bloodGroup) {
        this.bloodGroup = bloodGroup;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public void setLastDonationDate(String lastDonationDate) {
        this.lastDonationDate = lastDonationDate;
    }

    public void viewProfile(User user) {
        System.out.println();
        System.out.println();
        System.out.println("            MY PROFILE");
        System.out.println();
        System.out.println();
        System.out.println("User ID            : " + user.getUserId());
        System.out.println("Full Name          : " + user.getName());
        System.out.println("Age                : " + user.getAge());
        System.out.println("Gender             : " + user.getGender());
        System.out.println("Blood Group        : " + user.getBloodGroup());
        System.out.println("Phone Number       : " + user.getPhone());
        System.out.println("Email              : " + user.getEmail());
        System.out.println("Address            : " + user.getAddress());
        System.out.println("Username           : " + user.getUsername());
        System.out.println("Last Donation Date : " + user.getLastDonationDate());

        System.out.println("========================================");
    }

    @Override
    public String toString() {
        return "User{" +
                "userId=" + userId +
                ", name='" + name + '\'' +
                ", age=" + age +
                ", gender='" + gender + '\'' +
                ", bloodGroup='" + bloodGroup + '\'' +
                ", phone='" + phone + '\'' +
                ", email='" + email + '\'' +
                ", address='" + address + '\'' +
                ", username='" + username + '\'' +
                ", lastDonationDate='" + lastDonationDate + '\'' +
                '}';
    }

}


import java.sql.*;
import java.util.ArrayList;

public class UserManager {

    // ==============================
    // DS : ArrayList
    // ==============================

    private final ArrayList<User> users = new ArrayList<>();
    private int nextUserId = 1001;


    // ==============================
    // USER ID GENERATION
    // ==============================

    public int generateUserId() {
        return nextUserId++;
    }


    // ==============================
    // ADD USER - DS
    // ==============================

    public boolean addUser(User user) {

        if (user == null)
            return false;

        if (isUsernameExists(user.getUsername()))
            return false;

        if (user.getUserId() == 0)
            user.setUserId(generateUserId());

        users.add(user);

        return true;
    }


    // ==============================
    // CHECK USERNAME
    // ==============================

    public boolean isUsernameExists(String username) {

        if (username == null)
            return false;

        for (User user : users) {

            if (user.getUsername() != null &&
                    user.getUsername().equalsIgnoreCase(username)) {

                return true;
            }
        }

        return false;
    }


    // ==============================
    // SEARCH BY ID
    // ==============================

    public User searchById(int id) {

        for (User user : users) {

            if (user.getUserId() == id)
                return user;
        }

        return null;
    }


    // ==============================
    // SEARCH BY USERNAME
    // ==============================

    public User searchByUsername(String username) {

        if (username == null)
            return null;

        for (User user : users) {

            if (user.getUsername() != null &&
                    user.getUsername().equalsIgnoreCase(username)) {

                return user;
            }
        }

        return null;
    }


    // ==============================
    // UPDATE USER - DS
    // ==============================

    public boolean updateUser(User updatedUser) {

        if (updatedUser == null)
            return false;

        User existingUser = searchById(updatedUser.getUserId());

        if (existingUser == null)
            return false;

        existingUser.setName(updatedUser.getName());
        existingUser.setAge(updatedUser.getAge());
        existingUser.setGender(updatedUser.getGender());
        existingUser.setBloodGroup(updatedUser.getBloodGroup());
        existingUser.setPhone(updatedUser.getPhone());
        existingUser.setEmail(updatedUser.getEmail());
        existingUser.setAddress(updatedUser.getAddress());
        existingUser.setUsername(updatedUser.getUsername());
        existingUser.setPassword(updatedUser.getPassword());
        existingUser.setLastDonationDate(
                updatedUser.getLastDonationDate()
        );

        return true;
    }


    // ==============================
    // DELETE USER - DS
    // ==============================

    public boolean deleteUser(int id) {

        User user = searchById(id);

        if (user == null)
            return false;

        users.remove(user);

        return true;
    }


    // ==============================
    // TOTAL USERS
    // ==============================

    public int getTotalUsers() {
        return users.size();
    }


    // ==============================
    // DISPLAY ALL USERS
    // ==============================

    public void displayAllUsers() {

        if (users.isEmpty()) {

            System.out.println("No users found.");
            return;
        }

        System.out.println("----------------------------------------------");

        for (User user : users) {

            System.out.println(user);

            System.out.println("----------------------------------------------");
        }
    }


    // =====================================================
    // DATABASE / JDBC METHODS
    // =====================================================


    // ==============================
    // SAVE USER TO DATABASE
    // ==============================

    public boolean saveUserToDB(User user) {

        if (user == null)
            return false;

        String sql =
                "INSERT INTO users " +
                        "(user_id, name, age, gender, blood_group, phone, " +
                        "email, address, username, password, last_donation_date) " +
                        "VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)";

        try (Connection con = DatabaseConnection.getConnection();
             PreparedStatement pst = con.prepareStatement(sql)) {

            pst.setInt(1, user.getUserId());
            pst.setString(2, user.getName());
            pst.setInt(3, user.getAge());
            pst.setString(4, user.getGender());
            pst.setString(5, user.getBloodGroup());
            pst.setString(6, user.getPhone());
            pst.setString(7, user.getEmail());
            pst.setString(8, user.getAddress());
            pst.setString(9, user.getUsername());
            pst.setString(10, user.getPassword());
            pst.setString(11, user.getLastDonationDate());

            int rows = pst.executeUpdate();

            return rows > 0;

        } catch (SQLException e) {

            System.out.println("Error saving user: " + e.getMessage());
            return false;
        }
    }


    // ==============================
    // LOAD USERS FROM DATABASE
    // ==============================

    public void loadUsersFromDB() {

        String sql = "SELECT * FROM users";

        try (Connection con = DatabaseConnection.getConnection();
             PreparedStatement pst = con.prepareStatement(sql);
             ResultSet rs = pst.executeQuery()) {

            users.clear();

            while (rs.next()) {

                User user = new User();

                user.setUserId(rs.getInt("user_id"));
                user.setName(rs.getString("name"));
                user.setAge(rs.getInt("age"));
                user.setGender(rs.getString("gender"));
                user.setBloodGroup(rs.getString("blood_group"));
                user.setPhone(rs.getString("phone"));
                user.setEmail(rs.getString("email"));
                user.setAddress(rs.getString("address"));
                user.setUsername(rs.getString("username"));
                user.setPassword(rs.getString("password"));
                user.setLastDonationDate(
                        rs.getString("last_donation_date")
                );

                users.add(user);

                if (user.getUserId() >= nextUserId) {
                    nextUserId = user.getUserId() + 1;
                }
            }

        } catch (SQLException e) {

            System.out.println("Error loading users: " + e.getMessage());
        }
    }


    // ==============================
    // UPDATE USER IN DATABASE
    // ==============================

    public boolean updateUserInDB(User user) {

        if (user == null)
            return false;

        String sql =
                "UPDATE users SET " +
                        "name=?, age=?, gender=?, blood_group=?, phone=?, " +
                        "email=?, address=?, username=?, password=?, " +
                        "last_donation_date=? " +
                        "WHERE user_id=?";

        try (Connection con = DatabaseConnection.getConnection();
             PreparedStatement pst = con.prepareStatement(sql)) {

            pst.setString(1, user.getName());
            pst.setInt(2, user.getAge());
            pst.setString(3, user.getGender());
            pst.setString(4, user.getBloodGroup());
            pst.setString(5, user.getPhone());
            pst.setString(6, user.getEmail());
            pst.setString(7, user.getAddress());
            pst.setString(8, user.getUsername());
            pst.setString(9, user.getPassword());
            pst.setString(10, user.getLastDonationDate());
            pst.setInt(11, user.getUserId());

            int rows = pst.executeUpdate();

            return rows > 0;

        } catch (SQLException e) {

            System.out.println("Error updating user: " + e.getMessage());
            return false;
        }
    }


    // ==============================
    // DELETE USER FROM DATABASE
    // ==============================

    public boolean deleteUserFromDB(int id) {

        String sql = "DELETE FROM users WHERE user_id=?";

        try (Connection con = DatabaseConnection.getConnection();
             PreparedStatement pst = con.prepareStatement(sql)) {

            pst.setInt(1, id);

            int rows = pst.executeUpdate();

            return rows > 0;

        } catch (SQLException e) {

            System.out.println("Error deleting user: " + e.getMessage());
            return false;
        }
    }


    // ==============================
    // LOGIN CHECK
    // ==============================

    public User loginUser(String username, String password) {

        for (User user : users) {

            if (user.getUsername() != null &&
                    user.getPassword() != null &&
                    user.getUsername().equalsIgnoreCase(username) &&
                    user.getPassword().equals(password)) {

                return user;
            }
        }

        return null;
    }


    // ==============================
    // DATABASE LOGIN
    // ==============================

    public User loginUserFromDB(String username, String password) {

        String sql =
                "SELECT * FROM users " +
                        "WHERE username=? AND password=?";

        try (Connection con = DatabaseConnection.getConnection();
             PreparedStatement pst = con.prepareStatement(sql)) {

            pst.setString(1, username);
            pst.setString(2, password);

            try (ResultSet rs = pst.executeQuery()) {

                if (rs.next()) {

                    User user = new User();

                    user.setUserId(rs.getInt("user_id"));
                    user.setName(rs.getString("name"));
                    user.setAge(rs.getInt("age"));
                    user.setGender(rs.getString("gender"));
                    user.setBloodGroup(rs.getString("blood_group"));
                    user.setPhone(rs.getString("phone"));
                    user.setEmail(rs.getString("email"));
                    user.setAddress(rs.getString("address"));
                    user.setUsername(rs.getString("username"));
                    user.setPassword(rs.getString("password"));
                    user.setLastDonationDate(
                            rs.getString("last_donation_date")
                    );

                    return user;
                }
            }

        } catch (SQLException e) {

            System.out.println("Login error: " + e.getMessage());
        }

        return null;
    }
}

