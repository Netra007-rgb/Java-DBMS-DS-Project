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








































/// FINAL CODE 


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


import java.util.Scanner;

public class AdminMenu {

    Scanner sc=new Scanner(System.in);

    DonorManager donorManager=new DonorManager();
    RequestManager requestManager=new RequestManager();
    InventoryManager inventoryManager=new InventoryManager();

    public void showAdminMenu(){

        int choice;

        do{

            System.out.println("\n===== ADMIN MENU =====");
            System.out.println("1. Manage Donors");
            System.out.println("2. Manage Blood Requests");
            System.out.println("3. Manage Blood Inventory");
            System.out.println("4. Logout");

            System.out.print("Enter choice: ");
            choice=sc.nextInt();


            switch(choice){

                case 1:
                    donorMenu();
                    break;

                case 2:
                    requestMenu();
                    break;

                case 3:
                    inventoryMenu();
                    break;

                case 4:
                    System.out.println("Admin Logged Out");
                    break;

                default:
                    System.out.println("Invalid Choice");
            }

        }while(choice!=4);

    }


    public void donorMenu(){

        int choice;

        do{

            System.out.println("\n===== DONOR MANAGEMENT =====");
            System.out.println("1. Add Donor");
            System.out.println("2. Display Donors");
            System.out.println("3. Search Donor");
            System.out.println("4. Delete Donor");
            System.out.println("5. Back");

            System.out.print("Enter choice: ");
            choice=sc.nextInt();


            switch(choice){

                case 1:
                    donorManager.addDonor();
                    break;

                case 2:
                    donorManager.displayDonors();
                    break;

                case 3:
                    donorManager.searchDonor();
                    break;

                case 4:
                    donorManager.deleteDonor();
                    break;

                case 5:
                    break;

                default:
                    System.out.println("Invalid Choice");
            }


        }while(choice!=5);

    }


    public void requestMenu(){

        int choice;

        do{

            System.out.println("\n===== REQUEST MANAGEMENT =====");
            System.out.println("1. Add Blood Request");
            System.out.println("2. Display Requests");
            System.out.println("3. Update Request Status");
            System.out.println("4. Back");

            System.out.print("Enter choice: ");
            choice=sc.nextInt();


            switch(choice){

                case 1:
                    requestManager.addRequest();
                    break;

                case 2:
                    requestManager.displayRequests();
                    break;

                case 3:
                    requestManager.updateRequest();
                    break;

                case 4:
                    break;

                default:
                    System.out.println("Invalid Choice");
            }

        }while(choice!=4);

    }


    public void inventoryMenu(){

        int choice;

        do{

            System.out.println("\n===== INVENTORY MANAGEMENT =====");
            System.out.println("1. Display Inventory");
            System.out.println("2. Search Blood Stock");
            System.out.println("3. Update Inventory");
            System.out.println("4. Delete Inventory");
            System.out.println("5. Check Blood Availability");
            System.out.println("6. Back");

            System.out.print("Enter choice: ");
            choice=sc.nextInt();


            switch(choice){

                case 1:
                    inventoryManager.displayInventory();
                    break;

                case 2:
                    System.out.print("Enter Blood Group: ");
                    String group=sc.next();
                    inventoryManager.searchInventory(group);
                    break;

                case 3:
                    System.out.print("Enter Blood Group: ");
                    String bg=sc.next();

                    System.out.print("Enter New Units: ");
                    int units=sc.nextInt();

                    inventoryManager.updateInventory(bg,units);
                    break;

                case 4:
                    System.out.print("Enter Inventory ID: ");
                    int id=sc.nextInt();

                    inventoryManager.deleteInventory(id);
                    break;

                case 5:
                    System.out.print("Enter Blood Group: ");
                    String blood=sc.next();

                    System.out.print("Enter Required Units: ");
                    int required=sc.nextInt();

                    boolean result=inventoryManager.checkAvailability(blood,required);

                    if(result)
                        System.out.println("Blood Available");
                    else
                        System.out.println("Blood Not Available");

                    break;

                case 6:
                    break;

                default:
                    System.out.println("Invalid Choice");

            }

        }while(choice!=6);

    }

}





import java.sql.Connection;
import java.util.Scanner;

public class BloodDonorFinder {

    static Scanner sc = new Scanner(System.in);

    static UserManager userManager = new UserManager();
    static DonorManager donorManager = new DonorManager();
    static RequestManager requestManager = new RequestManager();
    static InventoryManager inventoryManager = new InventoryManager();

    public static void main(String[] args) {

        System.out.println("==============================================");
        System.out.println("        LIFELINK - BLOOD DONOR FINDER");
        System.out.println("==============================================");

        // Test Database Connection
        try {

            Connection con = DatabaseConnection.getConnection();

            if (con != null) {
                System.out.println("Database connected successfully.");
                DatabaseConnection.closeConnection(con);
            }

        } catch (Exception e) {

            System.out.println("Database connection failed.");
            System.out.println(e.getMessage());
        }

        int choice;

        do {

            System.out.println("\n==============================================");
            System.out.println("                MAIN MENU");
            System.out.println("==============================================");
            System.out.println("1. User Registration");
            System.out.println("2. User Login");
            System.out.println("3. Admin Login");
            System.out.println("4. Exit");

            System.out.print("Enter your choice: ");

            try {

                choice = sc.nextInt();
                sc.nextLine();

            } catch (Exception e) {

                System.out.println("Invalid input. Please enter a number.");
                sc.nextLine();
                choice = 0;
            }

            switch (choice) {

                // USER REGISTRATION

                case 1:
                    registerUser();
                    break;

                // USER LOGIN

                case 2:
                    userLogin();
                    break;

                // ADMIN LOGIN
                case 3:
                    adminLogin();
                    break;

                // EXIT
                case 4:
                    System.out.println("\nThank you for using LifeLink.");
                    System.out.println("Application closed successfully.");

                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        } while (choice != 4);

        sc.close();
    }

    // USER REGISTRATION

    public static void registerUser() {

        System.out.println("\n==============================================");
        System.out.println("              USER REGISTRATION");
        System.out.println("==============================================");

        User user = new User();

        System.out.print("Enter Name: ");
        user.setName(sc.nextLine());

        System.out.print("Enter Age: ");
        user.setAge(sc.nextInt());
        sc.nextLine();

        System.out.print("Enter Gender: ");
        user.setGender(sc.nextLine());

        System.out.print("Enter Blood Group: ");
        user.setBloodGroup(sc.nextLine().toUpperCase());

        System.out.print("Enter Phone Number: ");
        user.setPhone(sc.nextLine());

        System.out.print("Enter Email: ");
        user.setEmail(sc.nextLine());

        System.out.print("Enter Address: ");
        user.setAddress(sc.nextLine());

        System.out.print("Enter Username: ");
        String username = sc.nextLine();

        if (userManager.isUsernameExists(username)) {
            System.out.println("Username already exists.");
            return;
        }

        user.setUsername(username);

        System.out.print("Enter Password: ");
        user.setPassword(sc.nextLine());

        System.out.print("Enter Last Donation Date: ");
        user.setLastDonationDate(sc.nextLine());

        user.setUserId(userManager.generateUserId());

        boolean added = userManager.addUser(user);

        if (added) {
            System.out.println("\nUser registered successfully.");
            System.out.println("Your User ID is: " + user.getUserId());

            // Save user in database
            try {

                boolean saved = userManager.saveUserToDB(user);

                if (saved) {
                    System.out.println("User data saved to database.");
                } else {
                    System.out.println("Unable to save user data to database.");
                }

            } catch (Exception e) {
                System.out.println("Database Error: " + e.getMessage());
            }

        } else {
            System.out.println("User registration failed.");
        }
    }

    // USER LOGIN

    public static void userLogin() {

        System.out.println("\n==============================================");
        System.out.println("                 USER LOGIN");
        System.out.println("==============================================");

        System.out.print("Enter Username: ");
        String username = sc.nextLine();

        System.out.print("Enter Password: ");
        String password = sc.nextLine();

        User user = userManager.loginUser(username, password);

        // If user is not present in ArrayList,
        // check database
        if (user == null) {

            try {
                user = userManager.loginUserFromDB(username, password);
            } catch (Exception e) {
                System.out.println("Database Error: " + e.getMessage());
            }
        }

        if (user != null) {
            System.out.println("\nLogin Successful.");
            System.out.println("Welcome, " + user.getName() + "!");

            userMenu(user);
        } else {
            System.out.println("Invalid Username or Password.");
        }
    }

    // USER MENU

    public static void userMenu(User user) {
        int choice;
        do {

            System.out.println("\n==============================================");
            System.out.println("                 USER MENU");
            System.out.println("==============================================");

            System.out.println("1. Search Donor");
            System.out.println("2. View Blood Inventory");
            System.out.println("3. Search Blood Availability");
            System.out.println("4. Add Blood Request");
            System.out.println("5. View Blood Requests");
            System.out.println("6. Logout");

            System.out.print("Enter choice: ");

            try {
                choice = sc.nextInt();
                sc.nextLine();
            } catch (Exception e) {
                System.out.println("Invalid input.");
                sc.nextLine();
                choice = 0;
            }

            switch (choice) {

                // SEARCH DONOR
                case 1:
                    donorManager.searchDonor();
                    break;

                // VIEW INVENTORY
                case 2:
                    inventoryManager.displayInventory();
                    break;

                // SEARCH BLOOD AVAILABILITY
                case 3:
                    System.out.print("Enter Blood Group: ");
                    String bloodGroup = sc.nextLine().toUpperCase();

                    System.out.print("Enter Required Units: ");
                    int units = sc.nextInt();
                    sc.nextLine();

                    boolean available = inventoryManager.checkAvailability(bloodGroup, units);

                    if (available) {
                        System.out.println("Blood is available.");
                    } else {
                        System.out.println("Required blood is not available.");
                    }

                    break;

                // ADD BLOOD REQUEST
                case 4:
                    requestManager.addRequest();
                    break;

                // DISPLAY REQUESTS
                case 5:
                    requestManager.displayRequests();
                    break;

                // LOGOUT
                case 6:
                    System.out.println("User logged out successfully.");
                    break;

                default:
                    System.out.println("Invalid choice.");
            }

        } while (choice != 6);
    }

    // ADMIN LOGIN

    public static void adminLogin() {

        System.out.println("\n==============================================");
        System.out.println("                ADMIN LOGIN");
        System.out.println("==============================================");

        System.out.print("Enter Admin Username: ");
        String username = sc.nextLine();

        System.out.print("Enter Admin Password: ");
        String password = sc.nextLine();

        /*
         * Admin credentials for the project.
         *
         * Username : admin
         * Password : admin123
         */

        if (username.equals("admin") &&
                password.equals("admin123")) {

            System.out.println("\nAdmin Login Successful.");
            System.out.println("Welcome Administrator.");

            AdminMenu adminMenu = new AdminMenu();

            adminMenu.showAdminMenu();

        } else {
            System.out.println("Invalid Admin Username or Password.");
        }
    }
}



import java.sql.*;
import java.util.*;

public class BloodInventory {

    private int inventoryId;
    private String bloodGroup;
    private int unitsAvailable;
    private int minUnitsAvailability;

    // DS : ArrayList

    private static final ArrayList<BloodInventory> inventoryList = new ArrayList<>();


    public BloodInventory() {
    }

    public BloodInventory(int inventoryId, String bloodGroup, int unitsAvailable, int minUnitsAvailability) {
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


    // DS METHODS - ArrayList

    public static boolean addInventory(BloodInventory item) {

        if (item == null)
            return false;

        inventoryList.add(item);
        return true;
    }


    public static BloodInventory searchInventory(int id) {
        for (BloodInventory item : inventoryList) {
            if (item.getInventoryId() == id)
                return item;
        }

        return null;
    }


    public static boolean deleteInventory(int id) {
        BloodInventory item = searchInventory(id);
        if (item == null)
            return false;

        inventoryList.remove(item);
        return true;
    }


    public static void displayAllInventory() {

        if (inventoryList.isEmpty()) {
            System.out.println("No blood inventory available.");
            return;
        }

        for (BloodInventory item : inventoryList) {
            System.out.println(item);
        }
    }


    public static int getTotalInventoryRecords() {
        return inventoryList.size();
    }


// DBMS / JDBC

    // INSERT
    public boolean saveToDB() throws Exception {

        String sql = "INSERT INTO blood_inventory " +
                        "(inventory_id, blood_group, units_available, " +
                        "min_units_availability) VALUES (?, ?, ?, ?)";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/lifelink",
                "root",
                ""
        );

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setInt(1, inventoryId);
        pst.setString(2, bloodGroup);
        pst.setInt(3, unitsAvailable);
        pst.setInt(4, minUnitsAvailability);

        return pst.executeUpdate() > 0;
    }


    // SELECT
    public static void loadInventoryFromDB() throws Exception {

        String sql = "SELECT * FROM blood_inventory";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        Statement st = con.createStatement();

        ResultSet rs = st.executeQuery(sql);

        inventoryList.clear();

        while (rs.next()) {

            BloodInventory item = new BloodInventory();

            item.setInventoryId(rs.getInt("inventory_id"));

            item.setBloodGroup(rs.getString("blood_group"));

            item.setUnitsAvailable(rs.getInt("units_available"));

            item.setMinUnitsAvailability(rs.getInt("min_units_availability"));

            inventoryList.add(item);
        }

        System.out.println("Blood inventory loaded successfully.");
    }


    // UPDATE
    public boolean updateInDB() throws Exception {

        String sql = "UPDATE blood_inventory SET " +
                        "blood_group=?, units_available=?, " +
                        "min_units_availability=? " +
                        "WHERE inventory_id=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setString(1, bloodGroup);
        pst.setInt(2, unitsAvailable);
        pst.setInt(3, minUnitsAvailability);
        pst.setInt(4, inventoryId);

        return pst.executeUpdate() > 0;
    }


    // DELETE
    public static boolean deleteFromDB(int id) throws Exception {

        String sql = "DELETE FROM blood_inventory WHERE inventory_id=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setInt(1, id);

        return pst.executeUpdate() > 0;
    }


    @Override
    public String toString() {
        return "BloodInventory{" +
                "inventoryId=" + inventoryId +
                ", bloodGroup='" + bloodGroup + '\'' +
                ", unitsAvailable=" + unitsAvailable +
                ", minUnitsAvailability=" + minUnitsAvailability +
                '}';
    }}



    import java.sql.*;
import java.util.ArrayList;

// Blood request
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


    // DS : ArrayList

    private static final ArrayList<BloodRequest> requests
            = new ArrayList<>();


    public BloodRequest(int requestID, String patientName, int patientAge,
                        String bloodGroup, int unitsRequired,
                        String hospitalName, String cityName,
                        String contactNo, String requestStatus) {

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

    public int getDonorID() {
        return donorID;
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

    public String getPriority() {
        return priority;
    }

    public String getDonorName() {
        return donorName;
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

    public void setDonorName(String donorName) {
        this.donorName = donorName;
    }

    public void setPriority(String priority) {
        this.priority = priority;
    }

    public void setDonorID(int donorID) {
        this.donorID = donorID;
    }


    // DS METHODS - ArrayList

    public static boolean addRequest(BloodRequest request) {

        if (request == null)
            return false;

        requests.add(request);
        return true;
    }


    public static BloodRequest searchRequest(int id) {

        for (BloodRequest request : requests) {

            if (request.getRequestID() == id)
                return request;
        }

        return null;
    }


    public static boolean deleteRequest(int id) {

        BloodRequest request = searchRequest(id);

        if (request == null)
            return false;

        requests.remove(request);
        return true;
    }


    public static void displayAllRequests() {

        if (requests.isEmpty()) {

            System.out.println("No blood requests available.");
            return;
        }

        for (BloodRequest request : requests) {
            System.out.println(request);
        }
    }


    public static void displayPendingRequests() {

        boolean found = false;

        for (BloodRequest request : requests) {

            if ("Pending".equalsIgnoreCase(
                    request.getRequestStatus())) {

                System.out.println(request);
                found = true;
            }
        }

        if (!found)
            System.out.println("No pending requests.");
    }


    public static void displayCompletedRequests() {

        boolean found = false;

        for (BloodRequest request : requests) {

            if ("Completed".equalsIgnoreCase(
                    request.getRequestStatus())) {

                System.out.println(request);
                found = true;
            }
        }

        if (!found)
            System.out.println("No completed requests.");
    }


    public static void displayCriticalRequests() {

        boolean found = false;

        for (BloodRequest request : requests) {

            if ("High".equalsIgnoreCase(
                    request.getPriority())) {

                System.out.println(request);
                found = true;
            }
        }

        if (!found)
            System.out.println("No high priority requests.");
    }


    public static int getTotalRequests() {
        return requests.size();
    }


// DBMS / JDBC METHODS

    // INSERT
    public boolean saveToDB() throws Exception {

        String sql = "INSERT INTO blood_requests " +
                        "(request_id, patient_name, patient_age, blood_group, " +
                        "units_required, hospital_name, city_name, contact_no, " +
                        "request_status, donor_name, priority, donor_id) " +
                        "VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setInt(1, requestID);
        pst.setString(2, patientName);
        pst.setInt(3, patientAge);
        pst.setString(4, bloodGroup);
        pst.setInt(5, unitsRequired);
        pst.setString(6, hospitalName);
        pst.setString(7, cityName);
        pst.setString(8, contactNo);
        pst.setString(9, requestStatus);
        pst.setString(10, donorName);
        pst.setString(11, priority);
        pst.setInt(12, donorID);

        return pst.executeUpdate() > 0;
    }


    // SELECT
    public static void loadRequestsFromDB() throws Exception {

        String sql = "SELECT * FROM blood_requests";

        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        Statement st = con.createStatement();

        ResultSet rs = st.executeQuery(sql);

        requests.clear();

        while (rs.next()) {

            BloodRequest request =
                    new BloodRequest(
                            rs.getInt("request_id"),
                            rs.getString("patient_name"),
                            rs.getInt("patient_age"),
                            rs.getString("blood_group"),
                            rs.getInt("units_required"),
                            rs.getString("hospital_name"),
                            rs.getString("city_name"),
                            rs.getString("contact_no"),
                            rs.getString("request_status"));

            request.setDonorName(rs.getString("donor_name"));

            request.setPriority(rs.getString("priority"));

            request.setDonorID(rs.getInt("donor_id"));

            requests.add(request);
        }

        System.out.println("Blood requests loaded successfully.");
    }


    // UPDATE
    public boolean updateInDB() throws Exception {

        String sql = "UPDATE blood_requests SET " +
                        "patient_name=?, patient_age=?, blood_group=?, " +
                        "units_required=?, hospital_name=?, city_name=?, " +
                        "contact_no=?, request_status=?, donor_name=?, " +
                        "priority=?, donor_id=? " +
                        "WHERE request_id=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setString(1, patientName);
        pst.setInt(2, patientAge);
        pst.setString(3, bloodGroup);
        pst.setInt(4, unitsRequired);
        pst.setString(5, hospitalName);
        pst.setString(6, cityName);
        pst.setString(7, contactNo);
        pst.setString(8, requestStatus);
        pst.setString(9, donorName);
        pst.setString(10, priority);
        pst.setInt(11, donorID);
        pst.setInt(12, requestID);

        return pst.executeUpdate() > 0;
    }


    // DELETE
    public static boolean deleteFromDB(int id) throws Exception {

        String sql = "DELETE FROM blood_requests WHERE request_id=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);
        pst.setInt(1, id);

        return pst.executeUpdate() > 0;
    }


// STATUS METHODS

    public boolean cancelRequest() throws Exception {

        requestStatus = "Cancelled";

        return updateInDB();
    }


    public boolean completeRequest() throws Exception {

        requestStatus = "Completed";

        return updateInDB();
    }


    public boolean assignDonor(
            int donorID,
            String donorName) throws Exception {

        if ("Cancelled".equalsIgnoreCase(requestStatus) ||
                "Completed".equalsIgnoreCase(requestStatus)) {

            System.out.println("Cannot assign donor to this request.");

            return false;
        }

        this.donorID = donorID;
        this.donorName = donorName;
        this.requestStatus = "Assigned";

        return updateInDB();
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



import java.util.ArrayList;
import java.util.Scanner;
import java.sql.*;

public class BloodRequestService {

    private final ArrayList<BloodRequest> requests = new ArrayList<>();
    private Scanner sc = new Scanner(System.in);
    private int nextRequestId = 1;

    public BloodRequestService() {}

    public boolean addRequest(BloodRequest request) {
        if (request == null) {
            return false;
        }

        request.setRequestID(nextRequestId);
        nextRequestId++;
        request.setRequestStatus("Pending");
        requests.add(request);

        return true;
    }

    public BloodRequest searchRequest(int requestID) {
        for (BloodRequest request : requests) {
            if (request.getRequestID() == requestID) {
                return request;
            }
        }

        return null;
    }

    public boolean deleteRequest(int requestID) {
        BloodRequest request = searchRequest(requestID);
        if (request != null) {
            requests.remove(request);
            System.out.println("Request deleted successfully.");
            return true;
        }

        System.out.println("No matching requests found.");
        return false;
    }

    public void updateRequest() {
        System.out.println("Enter the Request ID you want to update:");
        int requestID = sc.nextInt();
        sc.nextLine();

        BloodRequest request = searchRequest(requestID);

        if (request == null) {
            System.out.println("No matching request found.");
            return;
        }

        int choice;

        do {
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

            switch (choice) {

                case 1:

                    System.out.print("Enter Updated Patient Name: ");

                    String patientName = sc.nextLine();

                    while (patientName.trim().isEmpty()) {

                        System.out.print("Name cannot be empty. Enter again: ");

                        patientName = sc.nextLine();
                    }

                    request.setPatientName(patientName);

                    System.out.println("Patient name updated successfully.");

                    break;


                case 2:

                    System.out.print("Enter Updated Patient Age: ");

                    int patientAge = sc.nextInt();

                    while (patientAge < 1 || patientAge > 110) {

                        System.out.print("Invalid age! Please enter age between 1 and 110: ");

                        patientAge = sc.nextInt();
                    }

                    request.setPatientAge(patientAge);

                    sc.nextLine();

                    System.out.println("Patient age updated successfully.");

                    break;


                case 3:

                    System.out.print("Enter Updated Blood Group: ");

                    String bloodGroup = sc.nextLine();

                    while (!(bloodGroup.equalsIgnoreCase("A+") ||
                            bloodGroup.equalsIgnoreCase("A-") ||
                            bloodGroup.equalsIgnoreCase("B+") ||
                            bloodGroup.equalsIgnoreCase("B-") ||
                            bloodGroup.equalsIgnoreCase("AB+") ||
                            bloodGroup.equalsIgnoreCase("AB-") ||
                            bloodGroup.equalsIgnoreCase("O+") ||
                            bloodGroup.equalsIgnoreCase("O-"))) {

                        System.out.print("Invalid Blood Group! Enter again: ");

                        bloodGroup = sc.nextLine();
                    }

                    request.setBloodGroup(bloodGroup.toUpperCase());

                    System.out.println("Blood group updated successfully.");

                    break;


                case 4:

                    System.out.print("Enter Updated Units Required: ");

                    int units = sc.nextInt();

                    while (units < 1 || units > 10) {

                        System.out.print("Units should be between 1 and 10: ");

                        units = sc.nextInt();
                    }

                    request.setUnitsRequired(units);

                    sc.nextLine();

                    System.out.println("Units updated successfully.");
                    break;


                case 5:
                    System.out.print("Enter Updated Hospital Name: ");

                    String hospital = sc.nextLine();

                    while (hospital.trim().isEmpty()) {

                        System.out.print("Hospital name cannot be empty. Enter again: ");

                        hospital = sc.nextLine();
                    }

                    request.setHospitalName(hospital);

                    System.out.println("Hospital name updated successfully.");

                    break;


                case 6:

                    System.out.print("Enter Updated City: ");

                    String city = sc.nextLine();

                    while (city.trim().isEmpty()) {

                        System.out.print("City name cannot be empty. Enter again: ");

                        city = sc.nextLine();
                    }

                    request.setCityName(city);

                    System.out.println("City updated successfully.");

                    break;


                case 7:

                    System.out.print("Enter Updated Contact Number: ");

                    String contact = sc.nextLine();

                    while (contact.length() != 10 ||
                            !Character.isDigit(contact.charAt(0)) ||
                            !Character.isDigit(contact.charAt(1)) ||
                            !Character.isDigit(contact.charAt(2)) ||
                            !Character.isDigit(contact.charAt(3)) ||
                            !Character.isDigit(contact.charAt(4)) ||
                            !Character.isDigit(contact.charAt(5)) ||
                            !Character.isDigit(contact.charAt(6)) ||
                            !Character.isDigit(contact.charAt(7)) ||
                            !Character.isDigit(contact.charAt(8)) ||
                            !Character.isDigit(contact.charAt(9))) {

                        System.out.print("Invalid Contact Number! Enter again: ");
                        contact = sc.nextLine();
                    }
                    request.setContactNo(contact);
                    System.out.println("Contact number updated successfully.");
                    break;


                case 8:

                    System.out.print("Enter Updated Priority (High/Medium/Low): ");
                    String priority = sc.nextLine();

                    while (!(priority.equalsIgnoreCase("High") ||
                            priority.equalsIgnoreCase("Medium") ||
                            priority.equalsIgnoreCase("Low"))) {

                        System.out.print("Invalid Priority! Enter High, Medium or Low: ");

                        priority = sc.nextLine();
                    }
                    request.setPriority(priority);
                    System.out.println("Priority updated successfully.");
                    break;

                case 9:

                    System.out.println("Exiting Update Menu...");
                    break;

                default:
                    System.out.println("Invalid choice.");
            }

        } while (choice != 9);
    }


    public void displayAllRequests() {

        if (requests.isEmpty()) {

            System.out.println("No requests available.");

            return;
        }

        for (BloodRequest request : requests) {

            System.out.println(request);
        }
    }


    public void displayPendingRequests() {

        boolean found = false;

        for (BloodRequest request : requests) {

            if ("Pending".equals(request.getRequestStatus())) {

                System.out.println(request);

                found = true;
            }
        }

        if (!found) {

            System.out.println("No pending requests.");
        }
    }


    public void displayCompletedRequests() {

        boolean found = false;

        for (BloodRequest request : requests) {

            if ("Completed".equals(request.getRequestStatus())) {
                System.out.println(request);
                found = true;
            }
        }

        if (!found) {
            System.out.println("No completed requests.");
        }
    }


    public boolean cancelRequest(int requestID) {

        BloodRequest request = searchRequest(requestID);

        if (request != null) {

            request.setRequestStatus("Cancelled");
            System.out.println("Request cancelled successfully.");

            return true;

        } else {

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


    public boolean assignDonor(
            int requestID,
            int donorID,
            String donorName) {

        BloodRequest request = searchRequest(requestID);

        if (request == null) {

            System.out.println("No matching requests found.");

            return false;

        } else if ("Cancelled".equals(request.getRequestStatus()) ||
                "Completed".equals(request.getRequestStatus())) {

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

// DATABASE / JDBC METHODS

// SAVE REQUEST TO DATABASE

    public boolean saveRequestToDB(BloodRequest request) throws Exception {

        if (request == null) {
            return false;
        }

        String sql = "INSERT INTO blood_requests " +
                        "(request_id, patient_name, patient_age, blood_group, " +
                        "units_required, hospital_name, city_name, contact_no, " +
                        "request_status, donor_name, priority, donor_id) " +
                        "VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setInt(1, request.getRequestID());
        pst.setString(2, request.getPatientName());
        pst.setInt(3, request.getPatientAge());
        pst.setString(4, request.getBloodGroup());
        pst.setInt(5, request.getUnitsRequired());
        pst.setString(6, request.getHospitalName());
        pst.setString(7, request.getCityName());
        pst.setString(8, request.getContactNo());
        pst.setString(9, request.getRequestStatus());
        pst.setString(10, request.getDonorName());
        pst.setString(11, request.getPriority());
        pst.setInt(12, request.getDonorID());

        int rows = pst.executeUpdate();

        pst.close();
        con.close();

        return rows > 0;
    }


// SEARCH REQUEST FROM DATABASE

    public BloodRequest searchRequestFromDB(int requestID) throws Exception {

        String sql =
                "SELECT * FROM blood_requests WHERE request_id=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/lifelink",
                "root",
                ""
        );

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setInt(1, requestID);

        ResultSet rs = pst.executeQuery();

        if (rs.next()) {

            BloodRequest request =
                    new BloodRequest(
                            rs.getInt("request_id"),
                            rs.getString("patient_name"),
                            rs.getInt("patient_age"),
                            rs.getString("blood_group"),
                            rs.getInt("units_required"),
                            rs.getString("hospital_name"),
                            rs.getString("city_name"),
                            rs.getString("contact_no"),
                            rs.getString("request_status"));

            request.setDonorName(rs.getString("donor_name"));

            request.setPriority(rs.getString("priority"));

            request.setDonorID(rs.getInt("donor_id"));

            rs.close();
            pst.close();
            con.close();

            return request;
        }

        rs.close();
        pst.close();
        con.close();

        return null;
    }


// DELETE REQUEST FROM DATABASE

    public boolean deleteRequestFromDB(int requestID) throws Exception {

        String sql = "DELETE FROM blood_requests " + "WHERE request_id=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setInt(1, requestID);

        int rows = pst.executeUpdate();

        pst.close();
        con.close();

        return rows > 0;
    }


// UPDATE REQUEST IN DATABASE

    public boolean updateRequestInDB(BloodRequest request) throws Exception {

        if (request == null) {
            return false;
        }

        String sql = "UPDATE blood_requests SET " +
                        "patient_name=?, patient_age=?, blood_group=?, " +
                        "units_required=?, hospital_name=?, city_name=?, " +
                        "contact_no=?, priority=? " +
                        "WHERE request_id=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setString(1, request.getPatientName());

        pst.setInt(2, request.getPatientAge());

        pst.setString(3, request.getBloodGroup());

        pst.setInt(4, request.getUnitsRequired());

        pst.setString(5, request.getHospitalName());

        pst.setString(6, request.getCityName());

        pst.setString(7, request.getContactNo());

        pst.setString(8, request.getPriority());

        pst.setInt(9, request.getRequestID());

        int rows = pst.executeUpdate();

        pst.close();
        con.close();

        return rows > 0;
    }


// UPDATE REQUEST STATUS IN DB

    public boolean updateRequestStatusInDB(int requestID, String status) throws Exception {

        String sql = "UPDATE blood_requests SET " + "request_status=? " + "WHERE request_id=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setString(1, status);

        pst.setInt(2, requestID);

        int rows = pst.executeUpdate();

        pst.close();
        con.close();

        return rows > 0;
    }


// ASSIGN DONOR IN DATABASE

    public boolean assignDonorInDB(int requestID, int donorID, String donorName) throws Exception {

        String sql = "UPDATE blood_requests SET " + "donor_id=?, donor_name=?, request_status=? " + "WHERE request_id=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setInt(1, donorID);

        pst.setString(2, donorName);

        pst.setString(3, "Assigned");

        pst.setInt(4, requestID);

        int rows = pst.executeUpdate();

        pst.close();
        con.close();

        return rows > 0;
    }


// LOAD ALL REQUESTS FROM DB

    public void loadRequestsFromDB() throws Exception {
        String sql = "SELECT * FROM blood_requests";

        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        Statement st = con.createStatement();

        ResultSet rs = st.executeQuery(sql);

        requests.clear();

        while (rs.next()) {

            BloodRequest request =
                    new BloodRequest(
                            rs.getInt("request_id"),
                            rs.getString("patient_name"),
                            rs.getInt("patient_age"),
                            rs.getString("blood_group"),
                            rs.getInt("units_required"),
                            rs.getString("hospital_name"),
                            rs.getString("city_name"),
                            rs.getString("contact_no"),
                            rs.getString("request_status"));

            request.setDonorName(rs.getString("donor_name"));

            request.setPriority(rs.getString("priority"));

            request.setDonorID(rs.getInt("donor_id"));

            requests.add(request);

            if (request.getRequestID() >= nextRequestId) {

                nextRequestId = request.getRequestID() + 1;
            }
        }

        rs.close();
        st.close();
        con.close();
        System.out.println("Blood requests loaded from database.");
    }
}



import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DatabaseConnection {
    //  Database Details
    private static final String URL = "jdbc:mysql://localhost:3306/lifelink";

    private static final String USER = "root";

    private static final String PASSWORD = "";


    // GET DATABASE CONNECTION

    public static Connection getConnection() {

        try {
            Connection con = DriverManager.getConnection(URL, USER, PASSWORD);
            return con;

        } catch (SQLException e) {

            System.out.println("Database connection failed!");
            System.out.println("Error: " + e.getMessage());

            return null;
        }
    }


    // CLOSE DATABASE CONNECTION

    public static void closeConnection(Connection con) {

        if (con != null) {
            try {
                con.close();
                System.out.println("Database connection closed.");
            }

            catch (SQLException e) {
                System.out.println("Error while closing connection: " + e.getMessage());
            }
        }
    }
}




import java.sql.*;
import java.util.ArrayList;


// this class stores donation history details
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


    // DS : ArrayList

    private static final ArrayList<DonationHistory> historyList
            = new ArrayList<>();


    public DonationHistory() {
    }

    public DonationHistory(int requestID, int historyID, int donorID,
                           String donorName, String patientName,
                           String bloodGroup, int unitsDonated,
                           String hospitalName, String cityName,
                           String donationDate) {

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


    // GETTERS

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


    // SETTERS

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


    // DS METHODS - ArrayList

    // ADD
    public static boolean addHistory(DonationHistory history) {

        if (history == null)
            return false;

        historyList.add(history);
        return true;
    }


    // SEARCH
    public static DonationHistory searchHistory(int historyID) {

        for (DonationHistory history : historyList) {

            if (history.getHistoryID() == historyID)
                return history;
        }

        return null;
    }


    // DELETE
    public static boolean deleteHistory(int historyID) {

        DonationHistory history = searchHistory(historyID);

        if (history == null)
            return false;

        historyList.remove(history);
        return true;
    }


    // DISPLAY ALL
    public static void displayAllHistory() {

        if (historyList.isEmpty()) {

            System.out.println("No donation history available.");
            return;
        }

        for (DonationHistory history : historyList) {
            System.out.println(history);
        }
    }


    // SEARCH BY DONOR
    public static void searchByDonor(int donorID) {

        boolean found = false;

        for (DonationHistory history : historyList) {

            if (history.getDonorID() == donorID) {

                System.out.println(history);
                found = true;
            }
        }

        if (!found) {
            System.out.println(
                    "No donation history found for this donor.");
        }
    }


    // TOTAL DONATION RECORDS
    public static int getTotalHistoryRecords() {
        return historyList.size();
    }


    // DBMS / JDBC METHODS

    // INSERT
    public boolean saveToDB() {

        String sql =
                "INSERT INTO donation_history " +
                        "(request_id, history_id, donor_id, donor_name, " +
                        "patient_name, blood_group, units_donated, " +
                        "hospital_name, city_name, donation_date) " +
                        "VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?)";

        try (Connection con = DatabaseConnection.getConnection();
             PreparedStatement pst = con.prepareStatement(sql)) {

            pst.setInt(1, requestID);
            pst.setInt(2, historyID);
            pst.setInt(3, donorID);
            pst.setString(4, donorName);
            pst.setString(5, patientName);
            pst.setString(6, bloodGroup);
            pst.setInt(7, unitsDonated);
            pst.setString(8, hospitalName);
            pst.setString(9, cityName);
            pst.setString(10, donationDate);

            return pst.executeUpdate() > 0;

        } catch (SQLException e) {

            System.out.println(
                    "Error saving donation history: "
                            + e.getMessage());

            return false;
        }
    }


    // SELECT
    public static void loadHistoryFromDB() {

        String sql = "SELECT * FROM donation_history";

        try (Connection con = DatabaseConnection.getConnection();
             PreparedStatement pst = con.prepareStatement(sql);
             ResultSet rs = pst.executeQuery()) {

            historyList.clear();

            while (rs.next()) {

                DonationHistory history =
                        new DonationHistory();

                history.setRequestID(
                        rs.getInt("request_id"));

                history.setHistoryID(
                        rs.getInt("history_id"));

                history.setDonorID(
                        rs.getInt("donor_id"));

                history.setDonorName(
                        rs.getString("donor_name"));

                history.setPatientName(
                        rs.getString("patient_name"));

                history.setBloodGroup(
                        rs.getString("blood_group"));

                history.setUnitsDonated(
                        rs.getInt("units_donated"));

                history.setHospitalName(
                        rs.getString("hospital_name"));

                history.setCityName(
                        rs.getString("city_name"));

                history.setDonationDate(
                        rs.getString("donation_date"));

                historyList.add(history);
            }

            System.out.println(
                    "Donation history loaded successfully.");

        } catch (SQLException e) {

            System.out.println(
                    "Error loading donation history: "
                            + e.getMessage());
        }
    }


    // UPDATE
    public boolean updateInDB() {

        String sql =
                "UPDATE donation_history SET " +
                        "request_id=?, donor_id=?, donor_name=?, " +
                        "patient_name=?, blood_group=?, units_donated=?, " +
                        "hospital_name=?, city_name=?, donation_date=? " +
                        "WHERE history_id=?";

        try (Connection con = DatabaseConnection.getConnection();
             PreparedStatement pst = con.prepareStatement(sql)) {

            pst.setInt(1, requestID);
            pst.setInt(2, donorID);
            pst.setString(3, donorName);
            pst.setString(4, patientName);
            pst.setString(5, bloodGroup);
            pst.setInt(6, unitsDonated);
            pst.setString(7, hospitalName);
            pst.setString(8, cityName);
            pst.setString(9, donationDate);
            pst.setInt(10, historyID);

            return pst.executeUpdate() > 0;

        } catch (SQLException e) {

            System.out.println(
                    "Error updating donation history: "
                            + e.getMessage());

            return false;
        }
    }


    // DELETE
    public static boolean deleteFromDB(int historyID) {

        String sql =
                "DELETE FROM donation_history WHERE history_id=?";

        try (Connection con = DatabaseConnection.getConnection();
             PreparedStatement pst = con.prepareStatement(sql)) {

            pst.setInt(1, historyID);

            return pst.executeUpdate() > 0;

        } catch (SQLException e) {

            System.out.println(
                    "Error deleting donation history: "
                            + e.getMessage());

            return false;
        }
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



import java.sql.*;
import java.util.InputMismatchException;
import java.util.Scanner;
import java.io.FileWriter;
import java.io.IOException;

//==============================================
// CUSTOM EXCEPTION
//==============================================

class InvalidDonorException extends Exception {

    public InvalidDonorException(String message) {
        super(message);
    }
}

//==============================================
// THREAD CLASS FOR FILE LOGGING
//==============================================

class LogThread extends Thread {

    private String message;

    public LogThread(String message) {
        this.message = message;
    }

    @Override
    public void run() {

        try {

            FileWriter fw = new FileWriter("DonorLog.txt", true);

            fw.write(message + "\n");

            fw.close();

        }

        catch (IOException e) {

            System.out.println("Unable to write into log file.");
        }
    }
}

//==============================================
// DONOR MANAGER
//==============================================

class DonorManager implements Manageable {

    Scanner sc = new Scanner(System.in);
    InventoryManager inventoryManager=new InventoryManager();

    public DonorManager() {
    }

    //------------------------------------------------------------
    // ADD DONOR
    //------------------------------------------------------------

    @Override
    public void addDonor() {

        System.out.println("Enter Donor's ID:");

        int donorID;

        while (true) {

            try {

                System.out.print("Enter Donor ID : ");
                donorID = sc.nextInt();
                sc.nextLine();
                break;

            } catch (InputMismatchException e) {

                System.out.println("Invalid Donor ID! Enter numbers only.");
                sc.nextLine();
            }
        }

        System.out.println("Enter Donor's Name:");
        String donorName = sc.nextLine();

        //--------------------------------------------------------

        int donorAge;

        while (true) {

            try {

                System.out.println("Enter Donor Age:");
                donorAge = sc.nextInt();
                sc.nextLine();

                if (donorAge >= 18 && donorAge <= 65) {

                    break;
                } else {

                    throw new InvalidDonorException("Age should be between 18 and 65.");
                }

            } catch (InputMismatchException e) {

                System.out.println("Age must be numeric.");
                sc.nextLine();
            } catch (InvalidDonorException e) {

                System.out.println(e.getMessage());
            }
        }

        //--------------------------------------------------------

        System.out.println("Enter Donor Gender:");
        String donorGender = sc.nextLine();

        //--------------------------------------------------------

        System.out.println("Enter Blood Group:");
        String bloodGroup = sc.nextLine().toUpperCase();

        while (true) {

            if (bloodGroup.equals("A+") ||
                    bloodGroup.equals("A-") ||
                    bloodGroup.equals("B+") ||
                    bloodGroup.equals("B-") ||
                    bloodGroup.equals("AB+") ||
                    bloodGroup.equals("AB-") ||
                    bloodGroup.equals("O+") ||
                    bloodGroup.equals("O-")) {

                break;
            } else {

                System.out.println("Invalid Blood Group.");

                bloodGroup = sc.nextLine().toUpperCase();
            }
        }

        //--------------------------------------------------------

        System.out.println("Enter City:");
        String cityName = sc.nextLine();

        //--------------------------------------------------------

        System.out.println("Enter Mobile Number:");

        String mobileNo = sc.nextLine();

        while (true) {

            if (mobileNo.length() != 10) {

                System.out.println("Invalid Mobile Number.");
                mobileNo = sc.nextLine();
            } else if (mobileNo.charAt(0) != '9' &&
                    mobileNo.charAt(0) != '8' &&
                    mobileNo.charAt(0) != '7' &&
                    mobileNo.charAt(0) != '6') {

                System.out.println("Invalid Mobile Number.");
                mobileNo = sc.nextLine();
            } else {

                break;
            }
        }

        //--------------------------------------------------------

        System.out.println("Enter Email:");

        String email = sc.nextLine();

        while (true) {

            if (email.contains("@") && email.contains(".")) {

                break;
            } else {

                System.out.println("Invalid Email.");
                email = sc.nextLine();
            }
        }

        //--------------------------------------------------------

        System.out.println("Enter Donation History:");
        String donorHistory = sc.nextLine();

        //--------------------------------------------------------

        boolean availability;

        while (true) {

            try {

                System.out.println("Enter Availability (true/false)");

                availability = sc.nextBoolean();
                sc.nextLine();

                break;

            } catch (InputMismatchException e) {

                System.out.println("Enter only true or false.");
                sc.nextLine();
            }
        }

        //--------------------------------------------------------

        Donor donor = new Donor(
                donorID,
                donorName,
                donorAge,
                donorGender,
                bloodGroup,
                cityName,
                mobileNo,
                email,
                donorHistory,
                availability
        );

        //--------------------------------------------------------
        // JDBC INSERT
        //--------------------------------------------------------

        Connection con = null;
        PreparedStatement pst = null;

        try {

            con = DatabaseConnection.getConnection();

            String sql = "INSERT INTO donor(donorID, donorName, donorAge, donorGender, bloodGroup, cityName, mobileNo, email, donorHistory, available) VALUES(?,?,?,?,?,?,?,?,?,?)";

            pst = con.prepareStatement(sql);

            pst.setInt(1, donor.getDonorID());
            pst.setString(2, donor.getDonorName());
            pst.setInt(3, donor.getDonorAge());
            pst.setString(4, donor.getDonorGender());
            pst.setString(5, donor.getBloodGroup());
            pst.setString(6, donor.getCityName());
            pst.setString(7, donor.getPhoneNo());
            pst.setString(8, donor.getEmail());
            pst.setString(9, donor.getDonorHistory());
            pst.setBoolean(10, donor.getAvailable());

            int rows = pst.executeUpdate();
            if (rows > 0) {
                System.out.println("Donor Successfully Added.");

                LogThread t = new LogThread("New Donor Added : " + donor.getDonorID());

                t.start();
                System.out.println("Enter Donated Blood Units:");

                int units=sc.nextInt();
                sc.nextLine();

                inventoryManager.increaseStock(donor.getBloodGroup(),units);
            } else {

                System.out.println("Insertion Failed.");
            }

        } catch (SQLException e) {

            System.out.println(e.getMessage());
        } finally {

            try {

                if (pst != null)
                    pst.close();

            } catch (SQLException e) {

                System.out.println(e.getMessage());
            }

            DatabaseConnection.closeConnection(con);
        }
    }

    @Override
    public void searchDonor() {

        int choice;

        do {

            System.out.println("\n========== SEARCH DONOR ==========");
            System.out.println("1. Search by Donor ID");
            System.out.println("2. Search by Blood Group");
            System.out.println("3. Search by City");
            System.out.println("4. Exit");
            System.out.print("Enter your Choice : ");

            try {

                choice = sc.nextInt();
                sc.nextLine();

            } catch (InputMismatchException e) {

                System.out.println("Invalid Choice! Enter numbers only.");
                sc.nextLine();
                choice = 0;
                continue;
            }

            Connection con = null;
            PreparedStatement pst = null;
            ResultSet rs = null;

            try {

                con = DatabaseConnection.getConnection();

                switch (choice) {

                    //==================================================
                    // SEARCH BY DONOR ID
                    //==================================================

                    case 1:

                        System.out.print("Enter Donor ID : ");

                        int donorID;

                        try {

                            donorID = sc.nextInt();
                            sc.nextLine();

                        } catch (InputMismatchException e) {

                            System.out.println("Invalid Donor ID!");
                            sc.nextLine();
                            break;
                        }

                        String sql1 =
                                "SELECT * FROM donor WHERE donorID=?";

                        pst = con.prepareStatement(sql1);

                        pst.setInt(1, donorID);

                        rs = pst.executeQuery();

                        if (rs.next()) {

                            System.out.println("\n------ DONOR FOUND ------");

                            System.out.println("Donor ID      : " + rs.getInt("donorID"));
                            System.out.println("Name          : " + rs.getString("donorName"));
                            System.out.println("Age           : " + rs.getInt("donorAge"));
                            System.out.println("Gender        : " + rs.getString("donorGender"));
                            System.out.println("Blood Group   : " + rs.getString("bloodGroup"));
                            System.out.println("City          : " + rs.getString("cityName"));
                            System.out.println("Mobile Number : " + rs.getString("mobileNo"));
                            System.out.println("Email         : " + rs.getString("email"));
                            System.out.println("History       : " + rs.getString("donorHistory"));
                            System.out.println("Available     : " + rs.getBoolean("available"));

                            LogThread t =
                                    new LogThread("Searched Donor ID : " + donorID);

                            t.start();

                        } else {

                            System.out.println("No Donor Found.");
                        }

                        break;

                    //==================================================
                    // SEARCH BY BLOOD GROUP
                    //==================================================

                    case 2:

                        System.out.print("Enter Blood Group : ");

                        String bloodGroup =
                                sc.nextLine().toUpperCase();

                        while (true) {

                            if (bloodGroup.equals("A+") ||
                                    bloodGroup.equals("A-") ||
                                    bloodGroup.equals("B+") ||
                                    bloodGroup.equals("B-") ||
                                    bloodGroup.equals("AB+") ||
                                    bloodGroup.equals("AB-") ||
                                    bloodGroup.equals("O+") ||
                                    bloodGroup.equals("O-")) {

                                break;
                            } else {

                                System.out.println("Invalid Blood Group.");
                                bloodGroup =
                                        sc.nextLine().toUpperCase();
                            }
                        }

                        String sql2 =
                                "SELECT * FROM donor WHERE bloodGroup=?";

                        pst = con.prepareStatement(sql2);

                        pst.setString(1, bloodGroup);

                        rs = pst.executeQuery();

                        boolean found = false;

                        while (rs.next()) {

                            found = true;

                            System.out.println("--------------------------------");

                            System.out.println("Donor ID : "
                                    + rs.getInt("donorID"));

                            System.out.println("Name : "
                                    + rs.getString("donorName"));

                            System.out.println("City : "
                                    + rs.getString("cityName"));

                            System.out.println("Mobile : "
                                    + rs.getString("mobileNo"));

                            System.out.println("Available : "
                                    + rs.getBoolean("available"));
                        }

                        if (!found) {

                            System.out.println("No Donor Found.");
                        } else {

                            LogThread t =
                                    new LogThread("Search By Blood Group : " + bloodGroup);

                            t.start();
                        }

                        break;

                    //==================================================
                    // SEARCH BY CITY
                    //==================================================

                    case 3:

                        System.out.print("Enter City : ");

                        String cityName = sc.nextLine();

                        String sql3 =
                                "SELECT * FROM donor WHERE cityName=?";

                        pst = con.prepareStatement(sql3);

                        pst.setString(1, cityName);

                        rs = pst.executeQuery();

                        boolean cityFound = false;

                        while (rs.next()) {

                            cityFound = true;

                            System.out.println("--------------------------------");

                            System.out.println("Donor ID : "
                                    + rs.getInt("donorID"));

                            System.out.println("Name : "
                                    + rs.getString("donorName"));

                            System.out.println("Blood Group : "
                                    + rs.getString("bloodGroup"));

                            System.out.println("Mobile : "
                                    + rs.getString("mobileNo"));

                            System.out.println("Available : "
                                    + rs.getBoolean("available"));
                        }

                        if (!cityFound) {

                            System.out.println("No Donor Found.");
                        } else {

                            LogThread t =
                                    new LogThread("Search By City : " + cityName);

                            t.start();
                        }

                        break;

                    case 4:

                        System.out.println("Exiting Search Menu...");
                        break;

                    default:

                        System.out.println("Invalid Choice.");

                }

            } catch (SQLException e) {

                System.out.println("Database Error : " + e.getMessage());

            } finally {

                try {

                    if (rs != null)
                        rs.close();

                    if (pst != null)
                        pst.close();

                } catch (SQLException e) {

                    System.out.println(e.getMessage());
                }

                DatabaseConnection.closeConnection(con);
            }

        }

        while (choice != 4);
    }

    @Override
    public void updateDonor() {

        System.out.println("Enter the Donor ID you want to update.");

        int updateDonorID;

        while (true) {

            try {

                updateDonorID = sc.nextInt();
                sc.nextLine();
                break;

            } catch (InputMismatchException e) {

                System.out.println("Invalid Donor ID.");
                sc.nextLine();
            }
        }

        Connection con = null;
        PreparedStatement pst = null;
        ResultSet rs = null;

        try {

            con = DatabaseConnection.getConnection();

            String check =
                    "SELECT * FROM donor WHERE donorID=?";

            pst = con.prepareStatement(check);

            pst.setInt(1, updateDonorID);

            rs = pst.executeQuery();

            if (!rs.next()) {

                System.out.println("Donor does not exist.");

                return;
            }

            pst.close();
            rs.close();

            int choice;

            do {

                System.out.println("\n========== UPDATE DONOR ==========");
                System.out.println("1. Update Name");
                System.out.println("2. Update Age");
                System.out.println("3. Update Mobile Number");
                System.out.println("4. Update Email");
                System.out.println("5. Update City");
                System.out.println("6. Update Availability");
                System.out.println("7. Exit");

                choice = sc.nextInt();
                sc.nextLine();

                switch (choice) {

                    //-----------------------------------------
                    // UPDATE NAME
                    //-----------------------------------------

                    case 1:

                        System.out.println("Enter Updated Name");

                        String donorName =
                                sc.nextLine();

                        String sql1 =
                                "UPDATE donor SET donorName=? WHERE donorID=?";

                        pst =
                                con.prepareStatement(sql1);

                        pst.setString(1, donorName);

                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {

                            System.out.println("Name Updated Successfully.");

                            LogThread t =
                                    new LogThread("Updated Name of Donor ID : " + updateDonorID);

                            t.start();
                        }

                        pst.close();

                        break;

                    //-----------------------------------------
                    // UPDATE AGE
                    //-----------------------------------------

                    case 2:

                        int donorAge;

                        while (true) {

                            try {

                                System.out.println("Enter Updated Age");

                                donorAge =
                                        sc.nextInt();

                                sc.nextLine();

                                if (donorAge >= 18 &&
                                        donorAge <= 65)

                                    break;

                                else

                                    throw new InvalidDonorException(
                                            "Age should be between 18 and 65.");

                            } catch (InputMismatchException e) {

                                System.out.println("Enter Numeric Age.");

                                sc.nextLine();
                            } catch (InvalidDonorException e) {

                                System.out.println(e.getMessage());
                            }
                        }

                        String sql2 =
                                "UPDATE donor SET donorAge=? WHERE donorID=?";

                        pst =
                                con.prepareStatement(sql2);

                        pst.setInt(1, donorAge);

                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {

                            System.out.println("Age Updated Successfully.");

                            LogThread t =
                                    new LogThread("Updated Age of Donor ID : " + updateDonorID);

                            t.start();
                        }

                        pst.close();

                        break;

                    //-----------------------------------------
                    // UPDATE MOBILE
                    //-----------------------------------------

                    case 3:

                        System.out.println("Enter Updated Mobile Number");

                        String mobileNo =
                                sc.nextLine();

                        while (true) {

                            if (mobileNo.length() != 10) {

                                System.out.println("Invalid Mobile Number");

                                mobileNo =
                                        sc.nextLine();
                            } else if (mobileNo.charAt(0) != '9' &&
                                    mobileNo.charAt(0) != '8' &&
                                    mobileNo.charAt(0) != '7' &&
                                    mobileNo.charAt(0) != '6') {

                                System.out.println("Invalid Mobile Number");

                                mobileNo =
                                        sc.nextLine();
                            } else

                                break;
                        }

                        String sql3 =
                                "UPDATE donor SET mobileNo=? WHERE donorID=?";

                        pst =
                                con.prepareStatement(sql3);

                        pst.setString(1, mobileNo);

                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {

                            System.out.println("Mobile Updated Successfully.");

                            LogThread t =
                                    new LogThread("Updated Mobile of Donor ID : " + updateDonorID);

                            t.start();
                        }

                        pst.close();

                        break;

                    //-----------------------------------------
                    // UPDATE EMAIL
                    //-----------------------------------------

                    case 4:

                        System.out.println("Enter Updated Email");

                        String email =
                                sc.nextLine();

                        while (true) {

                            if (email.contains("@")
                                    &&
                                    email.contains("."))

                                break;

                            else {

                                System.out.println("Invalid Email.");

                                email =
                                        sc.nextLine();
                            }
                        }

                        String sql4 =
                                "UPDATE donor SET email=? WHERE donorID=?";

                        pst =
                                con.prepareStatement(sql4);

                        pst.setString(1, email);

                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {
                            System.out.println("Email Updated Successfully.");
                            LogThread t = new LogThread("Updated Email of Donor ID : " + updateDonorID);
                            t.start();
                        }
                        pst.close();

                        break;
                    //-----------------------------------------
                    // UPDATE CITY
                    //-----------------------------------------

                    case 5:

                        System.out.println("Enter Updated City");

                        String cityName = sc.nextLine();
                        String sql5 = "UPDATE donor SET cityName=? WHERE donorID=?";
                        pst = con.prepareStatement(sql5);
                        pst.setString(1, cityName);
                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {
                            System.out.println("City Updated Successfully.");
                            LogThread t = new LogThread("Updated City of Donor ID : " + updateDonorID);
                            t.start();
                        }
                        pst.close();
                        break;
                    //-----------------------------------------
                    // UPDATE AVAILABILITY
                    //-----------------------------------------

                    case 6:

                        boolean available;
                        while (true) {

                            try {
                                System.out.println("Enter Updated Availability (true/false)");
                                available = sc.nextBoolean();
                                sc.nextLine();
                                break;
                            } catch (InputMismatchException e) {
                                System.out.println("Please Enter true or false.");
                                sc.nextLine();
                            }
                        }

                        String sql6 = "UPDATE donor SET available=? WHERE donorID=?";
                        pst = con.prepareStatement(sql6);
                        pst.setBoolean(1, available);
                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {
                            System.out.println("Availability Updated Successfully.");
                            LogThread t = new LogThread("Updated Availability of Donor ID : " + updateDonorID);
                            t.start();
                        }
                        pst.close();
                        break;
                    //-----------------------------------------
                    // EXIT
                    //-----------------------------------------

                    case 7:
                        System.out.println("Exiting Update Menu...");
                        break;
                    default:
                        System.out.println("Invalid Choice.");
                }

            }
            while (choice != 7);
        } catch (SQLException e) {
            System.out.println("Database Error : " + e.getMessage());
        } finally {

            try {
                if (rs != null)
                    rs.close();
                if (pst != null)
                    pst.close();
            } catch (SQLException e) {
                System.out.println(e.getMessage());
            }
            DatabaseConnection.closeConnection(con);
        }
    }

    @Override
    public void deleteDonor() {
        System.out.println("Enter the Donor ID you want to delete.");
        int donorID;

        while (true) {
            try {
                donorID = sc.nextInt();
                sc.nextLine();
                break;
            } catch (InputMismatchException e) {
                System.out.println("Invalid Donor ID.");
                sc.nextLine();
            }
        }
        Connection con = null;
        PreparedStatement pst = null;
        ResultSet rs = null;

        try {
            con = DatabaseConnection.getConnection();
            //-----------------------------------------
            // CHECK WHETHER DONOR EXISTS
            //-----------------------------------------
            String check = "SELECT * FROM donor WHERE donorID=?";
            pst = con.prepareStatement(check);
            pst.setInt(1, donorID);
            rs = pst.executeQuery();

            if (!rs.next()) {
                System.out.println("Donor Not Found.");
                return;
            }
            rs.close();
            pst.close();

            //-----------------------------------------
            // CONFIRMATION
            //-----------------------------------------

            System.out.println("Are you sure you want to delete this Donor? (YES/NO)");
            String result = sc.nextLine().toUpperCase();

            if (result.equals("YES")) {
                String sql = "DELETE FROM donor WHERE donorID=?";
                pst = con.prepareStatement(sql);
                pst.setInt(1, donorID);
                int rows = pst.executeUpdate();

                if (rows > 0) {

                    System.out.println("Donor Deleted Successfully.");
                    LogThread t = new LogThread("Deleted Donor ID : " + donorID);
                    t.start();
                } else {
                    System.out.println("Deletion Failed.");
                }
            } else if (result.equals("NO")) {
                System.out.println("Deletion Cancelled.");
            } else {
                System.out.println("Please Enter YES or NO.");
            }
        } catch (SQLException e) {
            System.out.println("Database Error : " + e.getMessage());
        } finally {
            try {
                if (rs != null)
                    rs.close();
                if (pst != null)
                    pst.close();
            } catch (SQLException e) {
                System.out.println(e.getMessage());
            }
            DatabaseConnection.closeConnection(con);
        }
    }

    @Override
    public void displayDonors() {

        System.out.println("\n========== DONOR LIST ==========");

        Connection con = null;
        PreparedStatement pst = null;
        ResultSet rs = null;

        try {

            con = DatabaseConnection.getConnection();

            String sql = "SELECT * FROM donor";
            pst = con.prepareStatement(sql);
            rs = pst.executeQuery();
            boolean found = false;

            while (rs.next()) {
                found = true;
                System.out.println("--------------------------------------------");
                System.out.println("Donor ID      : " + rs.getInt("donorID"));
                System.out.println("Name          : " + rs.getString("donorName"));
                System.out.println("Age           : " + rs.getInt("donorAge"));
                System.out.println("Gender        : " + rs.getString("donorGender"));
                System.out.println("Blood Group   : " + rs.getString("bloodGroup"));
                System.out.println("City          : " + rs.getString("cityName"));
                System.out.println("Mobile Number : " + rs.getString("mobileNo"));
                System.out.println("Email         : " + rs.getString("email"));
                System.out.println("History       : " + rs.getString("donorHistory"));
                System.out.println("Available     : " + rs.getBoolean("available"));
                System.out.println("--------------------------------------------");
            }

            if (!found) {
                System.out.println("No Donors Available.");
            } else {
                LogThread t = new LogThread("Displayed All Donors");
                t.start();
            }
        } catch (SQLException e) {

            System.out.println("Database Error : " +
                    e.getMessage());
        } finally {
            try {
                if (rs != null)
                    rs.close();
                if (pst != null)
                    pst.close();
            } catch (SQLException e) {
                System.out.println(e.getMessage());
            }
            DatabaseConnection.closeConnection(con);
        }
    }
}




import java.sql.*;
import java.util.InputMismatchException;
import java.util.Scanner;
import java.io.FileWriter;
import java.io.IOException;

//==============================================
// CUSTOM EXCEPTION
//==============================================

class InvalidDonorException extends Exception {

    public InvalidDonorException(String message) {
        super(message);
    }
}

//==============================================
// THREAD CLASS FOR FILE LOGGING
//==============================================

class LogThread extends Thread {

    private String message;

    public LogThread(String message) {
        this.message = message;
    }

    @Override
    public void run() {

        try {

            FileWriter fw = new FileWriter("DonorLog.txt", true);

            fw.write(message + "\n");

            fw.close();

        }

        catch (IOException e) {

            System.out.println("Unable to write into log file.");
        }
    }
}

//==============================================
// DONOR MANAGER
//==============================================

class DonorManager implements Manageable {

    Scanner sc = new Scanner(System.in);
    InventoryManager inventoryManager=new InventoryManager();

    public DonorManager() {
    }

    //------------------------------------------------------------
    // ADD DONOR
    //------------------------------------------------------------

    @Override
    public void addDonor() {

        System.out.println("Enter Donor's ID:");

        int donorID;

        while (true) {

            try {

                System.out.print("Enter Donor ID : ");
                donorID = sc.nextInt();
                sc.nextLine();
                break;

            } catch (InputMismatchException e) {

                System.out.println("Invalid Donor ID! Enter numbers only.");
                sc.nextLine();
            }
        }

        System.out.println("Enter Donor's Name:");
        String donorName = sc.nextLine();

        //--------------------------------------------------------

        int donorAge;

        while (true) {

            try {

                System.out.println("Enter Donor Age:");
                donorAge = sc.nextInt();
                sc.nextLine();

                if (donorAge >= 18 && donorAge <= 65) {

                    break;
                } else {

                    throw new InvalidDonorException("Age should be between 18 and 65.");
                }

            } catch (InputMismatchException e) {

                System.out.println("Age must be numeric.");
                sc.nextLine();
            } catch (InvalidDonorException e) {

                System.out.println(e.getMessage());
            }
        }

        //--------------------------------------------------------

        System.out.println("Enter Donor Gender:");
        String donorGender = sc.nextLine();

        //--------------------------------------------------------

        System.out.println("Enter Blood Group:");
        String bloodGroup = sc.nextLine().toUpperCase();

        while (true) {

            if (bloodGroup.equals("A+") ||
                    bloodGroup.equals("A-") ||
                    bloodGroup.equals("B+") ||
                    bloodGroup.equals("B-") ||
                    bloodGroup.equals("AB+") ||
                    bloodGroup.equals("AB-") ||
                    bloodGroup.equals("O+") ||
                    bloodGroup.equals("O-")) {

                break;
            } else {

                System.out.println("Invalid Blood Group.");

                bloodGroup = sc.nextLine().toUpperCase();
            }
        }

        //--------------------------------------------------------

        System.out.println("Enter City:");
        String cityName = sc.nextLine();

        //--------------------------------------------------------

        System.out.println("Enter Mobile Number:");

        String mobileNo = sc.nextLine();

        while (true) {

            if (mobileNo.length() != 10) {

                System.out.println("Invalid Mobile Number.");
                mobileNo = sc.nextLine();
            } else if (mobileNo.charAt(0) != '9' &&
                    mobileNo.charAt(0) != '8' &&
                    mobileNo.charAt(0) != '7' &&
                    mobileNo.charAt(0) != '6') {

                System.out.println("Invalid Mobile Number.");
                mobileNo = sc.nextLine();
            } else {

                break;
            }
        }

        //--------------------------------------------------------

        System.out.println("Enter Email:");

        String email = sc.nextLine();

        while (true) {

            if (email.contains("@") && email.contains(".")) {

                break;
            } else {

                System.out.println("Invalid Email.");
                email = sc.nextLine();
            }
        }

        //--------------------------------------------------------

        System.out.println("Enter Donation History:");
        String donorHistory = sc.nextLine();

        //--------------------------------------------------------

        boolean availability;

        while (true) {

            try {

                System.out.println("Enter Availability (true/false)");

                availability = sc.nextBoolean();
                sc.nextLine();

                break;

            } catch (InputMismatchException e) {

                System.out.println("Enter only true or false.");
                sc.nextLine();
            }
        }

        //--------------------------------------------------------

        Donor donor = new Donor(
                donorID,
                donorName,
                donorAge,
                donorGender,
                bloodGroup,
                cityName,
                mobileNo,
                email,
                donorHistory,
                availability
        );

        //--------------------------------------------------------
        // JDBC INSERT
        //--------------------------------------------------------

        Connection con = null;
        PreparedStatement pst = null;

        try {

            con = DatabaseConnection.getConnection();

            String sql = "INSERT INTO donor(donorID, donorName, donorAge, donorGender, bloodGroup, cityName, mobileNo, email, donorHistory, available) VALUES(?,?,?,?,?,?,?,?,?,?)";

            pst = con.prepareStatement(sql);

            pst.setInt(1, donor.getDonorID());
            pst.setString(2, donor.getDonorName());
            pst.setInt(3, donor.getDonorAge());
            pst.setString(4, donor.getDonorGender());
            pst.setString(5, donor.getBloodGroup());
            pst.setString(6, donor.getCityName());
            pst.setString(7, donor.getPhoneNo());
            pst.setString(8, donor.getEmail());
            pst.setString(9, donor.getDonorHistory());
            pst.setBoolean(10, donor.getAvailable());

            int rows = pst.executeUpdate();
            if (rows > 0) {
                System.out.println("Donor Successfully Added.");

                LogThread t = new LogThread("New Donor Added : " + donor.getDonorID());

                t.start();
                System.out.println("Enter Donated Blood Units:");

                int units=sc.nextInt();
                sc.nextLine();

                inventoryManager.increaseStock(donor.getBloodGroup(),units);
            } else {

                System.out.println("Insertion Failed.");
            }

        } catch (SQLException e) {

            System.out.println(e.getMessage());
        } finally {

            try {

                if (pst != null)
                    pst.close();

            } catch (SQLException e) {

                System.out.println(e.getMessage());
            }

            DatabaseConnection.closeConnection(con);
        }
    }

    @Override
    public void searchDonor() {

        int choice;

        do {

            System.out.println("\n========== SEARCH DONOR ==========");
            System.out.println("1. Search by Donor ID");
            System.out.println("2. Search by Blood Group");
            System.out.println("3. Search by City");
            System.out.println("4. Exit");
            System.out.print("Enter your Choice : ");

            try {

                choice = sc.nextInt();
                sc.nextLine();

            } catch (InputMismatchException e) {

                System.out.println("Invalid Choice! Enter numbers only.");
                sc.nextLine();
                choice = 0;
                continue;
            }

            Connection con = null;
            PreparedStatement pst = null;
            ResultSet rs = null;

            try {

                con = DatabaseConnection.getConnection();

                switch (choice) {

                    //==================================================
                    // SEARCH BY DONOR ID
                    //==================================================

                    case 1:

                        System.out.print("Enter Donor ID : ");

                        int donorID;

                        try {

                            donorID = sc.nextInt();
                            sc.nextLine();

                        } catch (InputMismatchException e) {

                            System.out.println("Invalid Donor ID!");
                            sc.nextLine();
                            break;
                        }

                        String sql1 =
                                "SELECT * FROM donor WHERE donorID=?";

                        pst = con.prepareStatement(sql1);

                        pst.setInt(1, donorID);

                        rs = pst.executeQuery();

                        if (rs.next()) {

                            System.out.println("\n------ DONOR FOUND ------");

                            System.out.println("Donor ID      : " + rs.getInt("donorID"));
                            System.out.println("Name          : " + rs.getString("donorName"));
                            System.out.println("Age           : " + rs.getInt("donorAge"));
                            System.out.println("Gender        : " + rs.getString("donorGender"));
                            System.out.println("Blood Group   : " + rs.getString("bloodGroup"));
                            System.out.println("City          : " + rs.getString("cityName"));
                            System.out.println("Mobile Number : " + rs.getString("mobileNo"));
                            System.out.println("Email         : " + rs.getString("email"));
                            System.out.println("History       : " + rs.getString("donorHistory"));
                            System.out.println("Available     : " + rs.getBoolean("available"));

                            LogThread t =
                                    new LogThread("Searched Donor ID : " + donorID);

                            t.start();

                        } else {

                            System.out.println("No Donor Found.");
                        }

                        break;

                    //==================================================
                    // SEARCH BY BLOOD GROUP
                    //==================================================

                    case 2:

                        System.out.print("Enter Blood Group : ");

                        String bloodGroup =
                                sc.nextLine().toUpperCase();

                        while (true) {

                            if (bloodGroup.equals("A+") ||
                                    bloodGroup.equals("A-") ||
                                    bloodGroup.equals("B+") ||
                                    bloodGroup.equals("B-") ||
                                    bloodGroup.equals("AB+") ||
                                    bloodGroup.equals("AB-") ||
                                    bloodGroup.equals("O+") ||
                                    bloodGroup.equals("O-")) {

                                break;
                            } else {

                                System.out.println("Invalid Blood Group.");
                                bloodGroup =
                                        sc.nextLine().toUpperCase();
                            }
                        }

                        String sql2 =
                                "SELECT * FROM donor WHERE bloodGroup=?";

                        pst = con.prepareStatement(sql2);

                        pst.setString(1, bloodGroup);

                        rs = pst.executeQuery();

                        boolean found = false;

                        while (rs.next()) {

                            found = true;

                            System.out.println("--------------------------------");

                            System.out.println("Donor ID : "
                                    + rs.getInt("donorID"));

                            System.out.println("Name : "
                                    + rs.getString("donorName"));

                            System.out.println("City : "
                                    + rs.getString("cityName"));

                            System.out.println("Mobile : "
                                    + rs.getString("mobileNo"));

                            System.out.println("Available : "
                                    + rs.getBoolean("available"));
                        }

                        if (!found) {

                            System.out.println("No Donor Found.");
                        } else {

                            LogThread t =
                                    new LogThread("Search By Blood Group : " + bloodGroup);

                            t.start();
                        }

                        break;

                    //==================================================
                    // SEARCH BY CITY
                    //==================================================

                    case 3:

                        System.out.print("Enter City : ");

                        String cityName = sc.nextLine();

                        String sql3 =
                                "SELECT * FROM donor WHERE cityName=?";

                        pst = con.prepareStatement(sql3);

                        pst.setString(1, cityName);

                        rs = pst.executeQuery();

                        boolean cityFound = false;

                        while (rs.next()) {

                            cityFound = true;

                            System.out.println("--------------------------------");

                            System.out.println("Donor ID : "
                                    + rs.getInt("donorID"));

                            System.out.println("Name : "
                                    + rs.getString("donorName"));

                            System.out.println("Blood Group : "
                                    + rs.getString("bloodGroup"));

                            System.out.println("Mobile : "
                                    + rs.getString("mobileNo"));

                            System.out.println("Available : "
                                    + rs.getBoolean("available"));
                        }

                        if (!cityFound) {

                            System.out.println("No Donor Found.");
                        } else {

                            LogThread t =
                                    new LogThread("Search By City : " + cityName);

                            t.start();
                        }

                        break;

                    case 4:

                        System.out.println("Exiting Search Menu...");
                        break;

                    default:

                        System.out.println("Invalid Choice.");

                }

            } catch (SQLException e) {

                System.out.println("Database Error : " + e.getMessage());

            } finally {

                try {

                    if (rs != null)
                        rs.close();

                    if (pst != null)
                        pst.close();

                } catch (SQLException e) {

                    System.out.println(e.getMessage());
                }

                DatabaseConnection.closeConnection(con);
            }

        }

        while (choice != 4);
    }

    @Override
    public void updateDonor() {

        System.out.println("Enter the Donor ID you want to update.");

        int updateDonorID;

        while (true) {

            try {

                updateDonorID = sc.nextInt();
                sc.nextLine();
                break;

            } catch (InputMismatchException e) {

                System.out.println("Invalid Donor ID.");
                sc.nextLine();
            }
        }

        Connection con = null;
        PreparedStatement pst = null;
        ResultSet rs = null;

        try {

            con = DatabaseConnection.getConnection();

            String check =
                    "SELECT * FROM donor WHERE donorID=?";

            pst = con.prepareStatement(check);

            pst.setInt(1, updateDonorID);

            rs = pst.executeQuery();

            if (!rs.next()) {

                System.out.println("Donor does not exist.");

                return;
            }

            pst.close();
            rs.close();

            int choice;

            do {

                System.out.println("\n========== UPDATE DONOR ==========");
                System.out.println("1. Update Name");
                System.out.println("2. Update Age");
                System.out.println("3. Update Mobile Number");
                System.out.println("4. Update Email");
                System.out.println("5. Update City");
                System.out.println("6. Update Availability");
                System.out.println("7. Exit");

                choice = sc.nextInt();
                sc.nextLine();

                switch (choice) {

                    //-----------------------------------------
                    // UPDATE NAME
                    //-----------------------------------------

                    case 1:

                        System.out.println("Enter Updated Name");

                        String donorName =
                                sc.nextLine();

                        String sql1 =
                                "UPDATE donor SET donorName=? WHERE donorID=?";

                        pst =
                                con.prepareStatement(sql1);

                        pst.setString(1, donorName);

                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {

                            System.out.println("Name Updated Successfully.");

                            LogThread t =
                                    new LogThread("Updated Name of Donor ID : " + updateDonorID);

                            t.start();
                        }

                        pst.close();

                        break;

                    //-----------------------------------------
                    // UPDATE AGE
                    //-----------------------------------------

                    case 2:

                        int donorAge;

                        while (true) {

                            try {

                                System.out.println("Enter Updated Age");

                                donorAge =
                                        sc.nextInt();

                                sc.nextLine();

                                if (donorAge >= 18 &&
                                        donorAge <= 65)

                                    break;

                                else

                                    throw new InvalidDonorException(
                                            "Age should be between 18 and 65.");

                            } catch (InputMismatchException e) {

                                System.out.println("Enter Numeric Age.");

                                sc.nextLine();
                            } catch (InvalidDonorException e) {

                                System.out.println(e.getMessage());
                            }
                        }

                        String sql2 =
                                "UPDATE donor SET donorAge=? WHERE donorID=?";

                        pst =
                                con.prepareStatement(sql2);

                        pst.setInt(1, donorAge);

                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {

                            System.out.println("Age Updated Successfully.");

                            LogThread t =
                                    new LogThread("Updated Age of Donor ID : " + updateDonorID);

                            t.start();
                        }

                        pst.close();

                        break;

                    //-----------------------------------------
                    // UPDATE MOBILE
                    //-----------------------------------------

                    case 3:

                        System.out.println("Enter Updated Mobile Number");

                        String mobileNo =
                                sc.nextLine();

                        while (true) {

                            if (mobileNo.length() != 10) {

                                System.out.println("Invalid Mobile Number");

                                mobileNo =
                                        sc.nextLine();
                            } else if (mobileNo.charAt(0) != '9' &&
                                    mobileNo.charAt(0) != '8' &&
                                    mobileNo.charAt(0) != '7' &&
                                    mobileNo.charAt(0) != '6') {

                                System.out.println("Invalid Mobile Number");

                                mobileNo =
                                        sc.nextLine();
                            } else

                                break;
                        }

                        String sql3 =
                                "UPDATE donor SET mobileNo=? WHERE donorID=?";

                        pst =
                                con.prepareStatement(sql3);

                        pst.setString(1, mobileNo);

                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {

                            System.out.println("Mobile Updated Successfully.");

                            LogThread t =
                                    new LogThread("Updated Mobile of Donor ID : " + updateDonorID);

                            t.start();
                        }

                        pst.close();

                        break;

                    //-----------------------------------------
                    // UPDATE EMAIL
                    //-----------------------------------------

                    case 4:

                        System.out.println("Enter Updated Email");

                        String email =
                                sc.nextLine();

                        while (true) {

                            if (email.contains("@")
                                    &&
                                    email.contains("."))

                                break;

                            else {

                                System.out.println("Invalid Email.");

                                email =
                                        sc.nextLine();
                            }
                        }

                        String sql4 =
                                "UPDATE donor SET email=? WHERE donorID=?";

                        pst =
                                con.prepareStatement(sql4);

                        pst.setString(1, email);

                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {
                            System.out.println("Email Updated Successfully.");
                            LogThread t = new LogThread("Updated Email of Donor ID : " + updateDonorID);
                            t.start();
                        }
                        pst.close();

                        break;
                    //-----------------------------------------
                    // UPDATE CITY
                    //-----------------------------------------

                    case 5:

                        System.out.println("Enter Updated City");

                        String cityName = sc.nextLine();
                        String sql5 = "UPDATE donor SET cityName=? WHERE donorID=?";
                        pst = con.prepareStatement(sql5);
                        pst.setString(1, cityName);
                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {
                            System.out.println("City Updated Successfully.");
                            LogThread t = new LogThread("Updated City of Donor ID : " + updateDonorID);
                            t.start();
                        }
                        pst.close();
                        break;
                    //-----------------------------------------
                    // UPDATE AVAILABILITY
                    //-----------------------------------------

                    case 6:

                        boolean available;
                        while (true) {

                            try {
                                System.out.println("Enter Updated Availability (true/false)");
                                available = sc.nextBoolean();
                                sc.nextLine();
                                break;
                            } catch (InputMismatchException e) {
                                System.out.println("Please Enter true or false.");
                                sc.nextLine();
                            }
                        }

                        String sql6 = "UPDATE donor SET available=? WHERE donorID=?";
                        pst = con.prepareStatement(sql6);
                        pst.setBoolean(1, available);
                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {
                            System.out.println("Availability Updated Successfully.");
                            LogThread t = new LogThread("Updated Availability of Donor ID : " + updateDonorID);
                            t.start();
                        }
                        pst.close();
                        break;
                    //-----------------------------------------
                    // EXIT
                    //-----------------------------------------

                    case 7:
                        System.out.println("Exiting Update Menu...");
                        break;
                    default:
                        System.out.println("Invalid Choice.");
                }

            }
            while (choice != 7);
        } catch (SQLException e) {
            System.out.println("Database Error : " + e.getMessage());
        } finally {

            try {
                if (rs != null)
                    rs.close();
                if (pst != null)
                    pst.close();
            } catch (SQLException e) {
                System.out.println(e.getMessage());
            }
            DatabaseConnection.closeConnection(con);
        }
    }

    @Override
    public void deleteDonor() {
        System.out.println("Enter the Donor ID you want to delete.");
        int donorID;

        while (true) {
            try {
                donorID = sc.nextInt();
                sc.nextLine();
                break;
            } catch (InputMismatchException e) {
                System.out.println("Invalid Donor ID.");
                sc.nextLine();
            }
        }
        Connection con = null;
        PreparedStatement pst = null;
        ResultSet rs = null;

        try {
            con = DatabaseConnection.getConnection();
            //-----------------------------------------
            // CHECK WHETHER DONOR EXISTS
            //-----------------------------------------
            String check = "SELECT * FROM donor WHERE donorID=?";
            pst = con.prepareStatement(check);
            pst.setInt(1, donorID);
            rs = pst.executeQuery();

            if (!rs.next()) {
                System.out.println("Donor Not Found.");
                return;
            }
            rs.close();
            pst.close();

            //-----------------------------------------
            // CONFIRMATION
            //-----------------------------------------

            System.out.println("Are you sure you want to delete this Donor? (YES/NO)");
            String result = sc.nextLine().toUpperCase();

            if (result.equals("YES")) {
                String sql = "DELETE FROM donor WHERE donorID=?";
                pst = con.prepareStatement(sql);
                pst.setInt(1, donorID);
                int rows = pst.executeUpdate();

                if (rows > 0) {

                    System.out.println("Donor Deleted Successfully.");
                    LogThread t = new LogThread("Deleted Donor ID : " + donorID);
                    t.start();
                } else {
                    System.out.println("Deletion Failed.");
                }
            } else if (result.equals("NO")) {
                System.out.println("Deletion Cancelled.");
            } else {
                System.out.println("Please Enter YES or NO.");
            }
        } catch (SQLException e) {
            System.out.println("Database Error : " + e.getMessage());
        } finally {
            try {
                if (rs != null)
                    rs.close();
                if (pst != null)
                    pst.close();
            } catch (SQLException e) {
                System.out.println(e.getMessage());
            }
            DatabaseConnection.closeConnection(con);
        }
    }

    @Override
    public void displayDonors() {

        System.out.println("\n========== DONOR LIST ==========");

        Connection con = null;
        PreparedStatement pst = null;
        ResultSet rs = null;

        try {

            con = DatabaseConnection.getConnection();

            String sql = "SELECT * FROM donor";
            pst = con.prepareStatement(sql);
            rs = pst.executeQuery();
            boolean found = false;

            while (rs.next()) {
                found = true;
                System.out.println("--------------------------------------------");
                System.out.println("Donor ID      : " + rs.getInt("donorID"));
                System.out.println("Name          : " + rs.getString("donorName"));
                System.out.println("Age           : " + rs.getInt("donorAge"));
                System.out.println("Gender        : " + rs.getString("donorGender"));
                System.out.println("Blood Group   : " + rs.getString("bloodGroup"));
                System.out.println("City          : " + rs.getString("cityName"));
                System.out.println("Mobile Number : " + rs.getString("mobileNo"));
                System.out.println("Email         : " + rs.getString("email"));
                System.out.println("History       : " + rs.getString("donorHistory"));
                System.out.println("Available     : " + rs.getBoolean("available"));
                System.out.println("--------------------------------------------");
            }

            if (!found) {
                System.out.println("No Donors Available.");
            } else {
                LogThread t = new LogThread("Displayed All Donors");
                t.start();
            }
        } catch (SQLException e) {

            System.out.println("Database Error : " +
                    e.getMessage());
        } finally {
            try {
                if (rs != null)
                    rs.close();
                if (pst != null)
                    pst.close();
            } catch (SQLException e) {
                System.out.println(e.getMessage());
            }
            DatabaseConnection.closeConnection(con);
        }
    }
}





import java.io.*;
import java.util.*;

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





import java.sql.*;

class InventoryManager {

    public void addInventory(BloodInventory inventory){

        try{
            Connection con=DatabaseConnection.getConnection();

            String query="insert into blood_inventory values(?,?,?,?)";

            PreparedStatement pst=con.prepareStatement(query);

            pst.setInt(1,inventory.getInventoryId());
            pst.setString(2,inventory.getBloodGroup());
            pst.setInt(3,inventory.getUnitsAvailable());
            pst.setInt(4,inventory.getMinUnitsAvailability());

            int result=pst.executeUpdate();

            if(result>0)
                System.out.println("Inventory Added Successfully");

            con.close();

        }catch(SQLException e){
            System.out.println(e);
        }
    }


    public void displayInventory(){

        try{
            Connection con=DatabaseConnection.getConnection();

            String query="select * from blood_inventory";

            PreparedStatement pst=con.prepareStatement(query);

            ResultSet rs=pst.executeQuery();

            while(rs.next()){

                System.out.println("Inventory ID: "+rs.getInt("inventory_id"));
                System.out.println("Blood Group: "+rs.getString("blood_group"));
                System.out.println("Units Available: "+rs.getInt("units_available"));
                System.out.println("Minimum Units: "+rs.getInt("min_units_availability"));
                System.out.println("-------------------");
            }

            con.close();

        }catch(SQLException e){
            System.out.println(e);
        }
    }


    public void searchInventory(String bloodGroup){

        try{
            Connection con=DatabaseConnection.getConnection();

            String query="select * from blood_inventory where blood_group=?";

            PreparedStatement pst=con.prepareStatement(query);

            pst.setString(1,bloodGroup);

            ResultSet rs=pst.executeQuery();

            if(rs.next()){

                System.out.println("Blood Group Found");
                System.out.println("Available Units: "+rs.getInt("units_available"));

            }
            else{
                System.out.println("Blood Not Available");
            }

            con.close();

        }catch(SQLException e){
            System.out.println(e);
        }
    }


    public void updateInventory(String bloodGroup,int units){

        try{

            Connection con=DatabaseConnection.getConnection();

            String query="update blood_inventory set units_available=? where blood_group=?";

            PreparedStatement pst=con.prepareStatement(query);

            pst.setInt(1,units);
            pst.setString(2,bloodGroup);

            int result=pst.executeUpdate();

            if(result>0)
                System.out.println("Inventory Updated");
            else
                System.out.println("Record Not Found");

            con.close();

        }catch(SQLException e){
            System.out.println(e);
        }
    }


    public void deleteInventory(int inventoryId){

        try{

            Connection con=DatabaseConnection.getConnection();

            String query="delete from blood_inventory where inventory_id=?";

            PreparedStatement pst=con.prepareStatement(query);

            pst.setInt(1,inventoryId);

            int result=pst.executeUpdate();

            if(result>0)
                System.out.println("Inventory Deleted");
            else
                System.out.println("Record Not Found");

            con.close();

        }catch(SQLException e){
            System.out.println(e);
        }
    }


    public boolean checkAvailability(String bloodGroup,int requiredUnits){

        try{

            Connection con=DatabaseConnection.getConnection();

            String query="select units_available from blood_inventory where blood_group=?";

            PreparedStatement pst=con.prepareStatement(query);

            pst.setString(1,bloodGroup);

            ResultSet rs=pst.executeQuery();


            if(rs.next()){

                int available=rs.getInt("units_available");

                if(available>=requiredUnits)
                    return true;
            }

            con.close();

        }catch(SQLException e){
            System.out.println(e);
        }

        return false;
    }


    public void decreaseStock(String bloodGroup,int units){

        try{

            Connection con=DatabaseConnection.getConnection();

            String query="update blood_inventory set units_available=units_available-? where blood_group=?";

            PreparedStatement pst=con.prepareStatement(query);

            pst.setInt(1,units);
            pst.setString(2,bloodGroup);

            pst.executeUpdate();

            System.out.println("Stock Updated");

            con.close();

        }catch(SQLException e){
            System.out.println(e);
        }
    }


    public void increaseStock(String bloodGroup,int units){

        try{

            Connection con=DatabaseConnection.getConnection();

            String query="update blood_inventory set units_available=units_available+? where blood_group=?";

            PreparedStatement pst=con.prepareStatement(query);

            pst.setInt(1,units);
            pst.setString(2,bloodGroup);

            pst.executeUpdate();

            System.out.println("Stock Increased");

            con.close();

        }catch(SQLException e){
            System.out.println(e);
        }
    }
}




public interface Manageable{
    public void addDonor();
    public void searchDonor();
    public void updateDonor();
    void deleteDonor();
    void displayDonors();
}







import java.sql.*;
import java.util.Scanner;

class RequestManager {

    Scanner sc=new Scanner(System.in);

    InventoryManager inventoryManager=new InventoryManager();


    public void addRequest(){

        try{

            Connection con=DatabaseConnection.getConnection();

            String query="insert into blood_request values(?,?,?,?,?,?,?,?,?)";

            PreparedStatement pst=con.prepareStatement(query);


            System.out.print("Enter Request ID: ");
            int id=sc.nextInt();

            System.out.print("Enter Patient Name: ");
            String name=sc.next();

            System.out.print("Enter Patient Age: ");
            int age=sc.nextInt();

            System.out.print("Enter Blood Group: ");
            String group=sc.next();

            System.out.print("Enter Required Units: ");
            int units=sc.nextInt();

            System.out.print("Enter Hospital Name: ");
            String hospital=sc.next();

            System.out.print("Enter City: ");
            String city=sc.next();

            System.out.print("Enter Contact Number: ");
            String contact=sc.next();


            pst.setInt(1,id);
            pst.setString(2,name);
            pst.setInt(3,age);
            pst.setString(4,group.toUpperCase());
            pst.setInt(5,units);
            pst.setString(6,hospital);
            pst.setString(7,city);
            pst.setString(8,contact);
            pst.setString(9,"Pending");


            int result=pst.executeUpdate();


            if(result>0)
                System.out.println("Request Added Successfully");


            con.close();


        }catch(SQLException e){
            System.out.println(e);
        }
    }



    public void displayRequests(){

        try{

            Connection con=DatabaseConnection.getConnection();

            String query="select * from blood_request";

            PreparedStatement pst=con.prepareStatement(query);

            ResultSet rs=pst.executeQuery();


            while(rs.next()){

                System.out.println("Request ID: "+rs.getInt("request_id"));
                System.out.println("Patient Name: "+rs.getString("patient_name"));
                System.out.println("Blood Group: "+rs.getString("blood_group"));
                System.out.println("Units Required: "+rs.getInt("units_required"));
                System.out.println("Status: "+rs.getString("request_status"));
                System.out.println("----------------------");

            }


            con.close();


        }catch(SQLException e){
            System.out.println(e);
        }

    }




    public void updateRequest(){

        try{

            Connection con=DatabaseConnection.getConnection();


            System.out.print("Enter Request ID: ");
            int id=sc.nextInt();


            String check="select * from blood_request where request_id=?";


            PreparedStatement checkStmt=con.prepareStatement(check);

            checkStmt.setInt(1,id);


            ResultSet rs=checkStmt.executeQuery();



            if(rs.next()){


                String group=rs.getString("blood_group");
                int units=rs.getInt("units_required");


                System.out.print("Enter New Status: ");
                String status=sc.next();



                String query="update blood_request set request_status=? where request_id=?";


                PreparedStatement pst=con.prepareStatement(query);


                pst.setString(1,status);
                pst.setInt(2,id);


                int result=pst.executeUpdate();



                if(result>0){

                    System.out.println("Request Updated");


                    if(status.equalsIgnoreCase("Approved")){

                        boolean available=inventoryManager.checkAvailability(group,units);


                        if(available){

                            inventoryManager.decreaseStock(group,units);

                            System.out.println("Inventory Updated");

                        }
                        else{

                            System.out.println("Insufficient Blood Stock");

                        }

                    }

                }


            }
            else{

                System.out.println("Request Not Found");

            }


            con.close();


        }catch(SQLException e){

            System.out.println(e);

        }

    }




    public void searchRequest(){

        try{

            Connection con=DatabaseConnection.getConnection();


            String query="select * from blood_request where blood_group=?";


            PreparedStatement pst=con.prepareStatement(query);


            System.out.print("Enter Blood Group: ");
            String group=sc.next();


            pst.setString(1,group.toUpperCase());


            ResultSet rs=pst.executeQuery();



            while(rs.next()){

                System.out.println("Patient Name: "+rs.getString("patient_name"));
                System.out.println("Hospital: "+rs.getString("hospital_name"));
                System.out.println("Status: "+rs.getString("request_status"));

            }


            con.close();


        }catch(SQLException e){

            System.out.println(e);

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

    // DS : ArrayList

    private final ArrayList<User> users = new ArrayList<>();
    private int nextUserId = 1001;


    // USER ID GENERATION

    public int generateUserId() {
        return nextUserId++;
    }

    // ADD USER - DS

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


    // CHECK USERNAME

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


    // SEARCH BY ID

    public User searchById(int id) {
        for (User user : users) {
            if (user.getUserId() == id)
                return user;
        }

        return null;
    }


    // SEARCH BY USERNAME

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


    // UPDATE USER - DS

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


    // DELETE USER - DS

    public boolean deleteUser(int id) {
        User user = searchById(id);
        if (user == null)
            return false;

        users.remove(user);

        return true;
    }


    // TOTAL USERS

    public int getTotalUsers() {
        return users.size();
    }


    // DISPLAY ALL USERS

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


    // DATABASE / JDBC METHODS


// SAVE USER TO DATABASE

    public boolean saveUserToDB(User user) throws Exception {

        if (user == null)
            return false;

        String sql = "INSERT INTO users " +
                        "(user_id, name, age, gender, blood_group, phone, " +
                        "email, address, username, password, last_donation_date) " +
                        "VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

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
    }


// LOAD USERS FROM DATABASE

    public void loadUsersFromDB() throws Exception {

        String sql = "SELECT * FROM users";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        Statement st = con.createStatement();

        ResultSet rs = st.executeQuery(sql);

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

            user.setLastDonationDate(rs.getString("last_donation_date"));

            users.add(user);

            if (user.getUserId() >= nextUserId) {
                nextUserId = user.getUserId() + 1;
            }
        }
    }


// UPDATE USER IN DATABASE

    public boolean updateUserInDB(User user) throws Exception {

        if (user == null)
            return false;

        String sql = "UPDATE users SET " +
                        "name=?, age=?, gender=?, blood_group=?, phone=?, " +
                        "email=?, address=?, username=?, password=?, " +
                        "last_donation_date=? " +
                        "WHERE user_id=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

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
    }


// DELETE USER FROM DATABASE

    public boolean deleteUserFromDB(int id) throws Exception {

        String sql = "DELETE FROM users WHERE user_id=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setInt(1, id);

        int rows = pst.executeUpdate();

        return rows > 0;
    }


// LOGIN CHECK

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


// DATABASE LOGIN

    public User loginUserFromDB(
            String username,
            String password) throws Exception {

        String sql = "SELECT * FROM users " + "WHERE username=? AND password=?";

        Class.forName("com.mysql.cj.jdbc.Driver");

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink", "root", "");

        PreparedStatement pst = con.prepareStatement(sql);

        pst.setString(1, username);
        pst.setString(2, password);

        ResultSet rs = pst.executeQuery();

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

            user.setLastDonationDate(rs.getString("last_donation_date"));

            return user;
        }

        return null;
    }
}



