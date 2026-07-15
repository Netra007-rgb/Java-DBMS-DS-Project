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
