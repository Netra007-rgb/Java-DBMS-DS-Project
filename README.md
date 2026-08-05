//java+ds+dbms project

package model;

//Admin Class

public class Admin{ int adminId; String adminName; String userName; String password; String email; String phoneNo;

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

//blood inventory class

package model;
import java.sql.*;
import java.util.*;

public class BloodInventory {

    private int inventoryId;
    private String bloodGroup;
    private int unitsAvailable;
    private int minUnitsAvailability;

    // DS : LinkedList

    private static final LinkedList<BloodInventory> inventoryList = new LinkedList<>();

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

    // DS METHODS - LinkedList

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

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink1","root","");

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

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink1","root","");

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

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink1", "root", "");

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

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink1", "root", "");

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
    }
}

//blood request class

//this class only stores blood request data
package model;

import database.DatabaseConnection;
// Blood request
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

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink1", "root", "");

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
        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink1", "root", "");

        Statement st = con.createStatement();

        ResultSet rs = st.executeQuery(sql);

        requests.clear();

        while (rs.next()) {

            BloodRequest request = new BloodRequest(
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

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink1", "root", "");

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

        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/lifelink1", "root", "");

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

//donation history class

package model;
import database.DatabaseConnection;

import java.sql.*;
import java.util.*;

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


    // DS : HashMap

    private static final HashMap<Integer, DonationHistory> historyMap = new HashMap<>();

    public DonationHistory() {}

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


    // DS METHODS - HashMap

    // ADD
    public static boolean addHistory(DonationHistory history) {

        if (history == null)
            return false;

        if (historyMap.containsKey(history.getHistoryID()))
            return false;

        historyMap.put(history.getHistoryID(), history);
        return true;
    }


    // SEARCH
    public static DonationHistory searchHistory(int historyID) {
        return historyMap.get(historyID);
    }


    // DELETE
    public static boolean deleteHistory(int historyID) {
        if (!historyMap.containsKey(historyID))
            return false;

        historyMap.remove(historyID);

        return true;
    }


    // DISPLAY ALL
    public static void displayAllHistory() {

        if (historyMap.isEmpty()) {
            System.out.println("No donation history available.");
            return;
        }

        for (DonationHistory history : historyMap.values()) {
            System.out.println(history);
        }
    }


    // SEARCH BY DONOR
    public static void searchByDonor(int donorID) {
        boolean found = false;

        for (DonationHistory history : historyMap.values()) {
            if (history.getDonorID() == donorID) {

                System.out.println(history);
                found = true;
            }
        }

        if (!found) {
            System.out.println("No donation history found for this donor.");
        }
    }

    // TOTAL DONATION RECORDS
    public static int getTotalHistoryRecords() {
        return historyMap.size();
    }


    // DBMS / JDBC METHODS

    // INSERT
    public boolean saveToDB() {

        String sql = "INSERT INTO donation_history " +
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
            System.out.println("Error saving donation history: " + e.getMessage());

            return false;
        }
    }


    // SELECT
    public static void loadHistoryFromDB() {

        String sql = "SELECT * FROM donation_history";

        try (Connection con = DatabaseConnection.getConnection();
             PreparedStatement pst = con.prepareStatement(sql);
             ResultSet rs = pst.executeQuery()) {

            historyMap.clear();

            while (rs.next()) {
                DonationHistory history = new DonationHistory();

                history.setRequestID(rs.getInt("request_id"));

                history.setHistoryID(rs.getInt("history_id"));

                history.setDonorID(rs.getInt("donor_id"));

                history.setDonorName(rs.getString("donor_name"));

                history.setPatientName(rs.getString("patient_name"));

                history.setBloodGroup(rs.getString("blood_group"));

                history.setUnitsDonated(rs.getInt("units_donated"));

                history.setHospitalName(rs.getString("hospital_name"));

                history.setCityName(rs.getString("city_name"));

                history.setDonationDate(rs.getString("donation_date"));

                historyMap.put(history.getHistoryID(),history
                );
            }

            System.out.println("Donation history loaded successfully.");

        } catch (SQLException e) {
            System.out.println("Error loading donation history: " +e.getMessage());
        }
    }


    // UPDATE
    public boolean updateInDB() {

        String sql = "UPDATE donation_history SET " +
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
            System.out.println("Error updating donation history: " +e.getMessage());

            return false;
        }
    }


    // DELETE
    public static boolean deleteFromDB(int historyID) {

        String sql = "DELETE FROM donation_history WHERE history_id=?";

        try (Connection con = DatabaseConnection.getConnection();
             PreparedStatement pst = con.prepareStatement(sql))
        {
            pst.setInt(1, historyID);
            return pst.executeUpdate() > 0;

        } catch (SQLException e) {
            System.out.println("Error deleting donation history: " +e.getMessage());
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

//donor class

package model;

//Donor Class
public class Donor{ int donorID; String donorName; int donorAge; String donorGender; String bloodGroup; String cityName; String phoneNo; String email; String donorHistory; Boolean available;

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


//user class

package model;

public class User{

    private int userId;
    private String name;
    private int age;
    private String gender;
    private String bloodGroup;
    private String role;
    private String phone;
    private String email;
    private String address;
    private String username;
    private String password;
    private String lastDonationDate;

    public User() {}

    public User(int userId,
                String name,
                int age,
                String gender,
                String bloodGroup,
                String role,
                String phone,
                String email,
                String address,
                String username,
                String password,
                String lastDonationDate) {

        this.userId = userId;
        this.name = name;
        this.age = age;
        this.gender = gender;
        this.bloodGroup = bloodGroup;
        this.role = role;
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

    public String getRole() {
        return role;
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

    public void setRole(String role) {
        this.role = role;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public void setLastDonationDate(String lastDonationDate) {
        this.lastDonationDate = lastDonationDate;
    }

    @Override
    public String toString() {

        return "User ID          : " + userId +
                "\nName             : " + name +
                "\nAge              : " + age +
                "\nGender           : " + gender +
                "\nBlood Group      : " + bloodGroup +
                "\nRole             : " + role +
                "\nPhone            : " + phone +
                "\nEmail            : " + email +
                "\nAddress          : " + address +
                "\nUsername         : " + username +
                "\nLast Donation    : " + lastDonationDate;
    }
}

//donation history class

package service;

import model.DonationHistory;

import java.util.ArrayList;
import java.util.Scanner;
import java.io.FileWriter;
import java.io.IOException;

public class DonationHistoryService {
    private final ArrayList<DonationHistory> historyList = new ArrayList<>();
    private final Scanner sc = new Scanner(System.in);

    private int nextHistoryID = 1;

    public DonationHistoryService() {
    }

    // Add Donation History
    public boolean addDonationHistory(DonationHistory history) {
        if (history == null) {
            System.out.println("Invalid donation history.");
            return false;
        }
        try {
            history.setHistoryID(nextHistoryID++);
            historyList.add(history);
            try (FileWriter fw = new FileWriter("DonationHistoryLog.txt", true)) {

                fw.write("History ID : " + history.getHistoryID()
                        + " | Donor : " + history.getDonorName() + "\n");
            } catch (IOException e) {
                System.out.println("Unable to update log file.");
            }
            // JDBC - SAVE TO DATABASE

            boolean saved = history.saveToDB();

            if (saved) {
                System.out.println("Donation history saved to database.");
            } else {
                System.out.println("Unable to save donation history to database.");
            }

            System.out.println("Donation history added successfully.");
            return true;

        } catch (Exception e) {
            System.out.println("Unable to add donation history.");
            return false;
        }
    }

    // Search Donation History
    public DonationHistory searchHistory(int historyID) {

        for (DonationHistory history : historyList) {

            if (history.getHistoryID() == historyID) {
                return history;
            }
        }
        return null;
    }

    // Delete Donation History
    public boolean deleteHistory(int historyID) {

        DonationHistory history = searchHistory(historyID);

        if (history == null) {
            System.out.println("No matching history found.");
            return false;
        }

        historyList.remove(history);

        try (FileWriter fw = new FileWriter("DonationHistoryLog.txt", true)) {

            fw.write("Deleted History ID : " + historyID + "\n");

        } catch (IOException e) {
            System.out.println("Unable to update log file.");
        }

        boolean deleted = DonationHistory.deleteFromDB(historyID);

        if (deleted) {
            System.out.println("Donation history deleted from database.");
        } else {
            System.out.println("Unable to delete donation history from database.");
        }

        System.out.println("History deleted successfully.");
        return true;
    }
}

//donor manager class

package service;

import database.DatabaseConnection;
import model.Donor;
import java.sql.*;
import java.util.InputMismatchException;
import java.util.Scanner;
import java.io.FileWriter;
import java.io.IOException;


// CUSTOM EXCEPTION

class InvalidDonorException extends Exception {
    public InvalidDonorException(String message) {
        super(message);
    }
}

// THREAD CLASS FOR FILE LOGGING

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

// DONOR MANAGER

public class DonorManager implements Manageable {

    Scanner sc = new Scanner(System.in);
    InventoryManager inventoryManager = new InventoryManager();

    public DonorManager() {
    }

    // ADD DONOR

    @Override
    public void addDonor() {
        //System.out.println("Enter Donor's ID:");
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

            String sql = "INSERT INTO donor(donor_id, donor_name, donor_age, donor_gender, blood_group," +
                    "city_name, phone_no, email, donor_history, available) VALUES(?,?,?,?,?,?,?,?,?,?)";

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

                int units = sc.nextInt();
                sc.nextLine();

                inventoryManager.increaseStock(donor.getBloodGroup(), units);
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

                        String sql1 = "SELECT * FROM donor WHERE donor_id=?";
                        pst = con.prepareStatement(sql1);
                        pst.setInt(1, donorID);

                        rs = pst.executeQuery();

                        if (rs.next()) {

                            System.out.println("\n------ DONOR FOUND ------");

                            System.out.println("Donor ID      : " + rs.getInt("donor_id"));
                            System.out.println("Name          : " + rs.getString("donor_name"));
                            System.out.println("Age           : " + rs.getInt("donor_age"));
                            System.out.println("Gender        : " + rs.getString("donor_gender"));
                            System.out.println("Blood Group   : " + rs.getString("blood_group"));
                            System.out.println("City          : " + rs.getString("city_name"));
                            System.out.println("Mobile Number : " + rs.getString("phone_no"));
                            System.out.println("Email         : " + rs.getString("email"));
                            System.out.println("History       : " + rs.getString("donor_history"));
                            System.out.println("Available     : " + rs.getBoolean("available"));

                            LogThread t = new LogThread("Searched Donor ID : " + donorID);
                            t.start();


                        } else {
                            System.out.println("No Donor Found.");
                        }
                        break;

                    // SEARCH BY BLOOD GROUP

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

                        String sql2 = "SELECT * FROM donor WHERE blood_group=?";

                        pst = con.prepareStatement(sql2);
                        pst.setString(1, bloodGroup);

                        rs = pst.executeQuery();

                        boolean found = false;

                        while (rs.next()) {
                            found = true;

                            System.out.println("--------------------------------");

                            System.out.println("Donor ID : " + rs.getInt("donor_id"));

                            System.out.println("Name : " + rs.getString("donor_name"));

                            System.out.println("City : " + rs.getString("city_name"));

                            System.out.println("Mobile : " + rs.getString("phone_no"));

                            System.out.println("Available : " + rs.getBoolean("available"));
                        }

                        if (!found) {
                            System.out.println("No Donor Found.");
                        } else {
                            LogThread t = new LogThread("Search By Blood Group : " + bloodGroup);
                            t.start();
                        }

                        break;

                    // SEARCH BY CITY

                    case 3:

                        System.out.print("Enter City : ");
                        String cityName = sc.nextLine();

                        String sql3 = "SELECT * FROM donor WHERE city_name=?";
                        pst = con.prepareStatement(sql3);

                        pst.setString(1, cityName);

                        rs = pst.executeQuery();
                        boolean cityFound = false;

                        while (rs.next()) {

                            cityFound = true;

                            System.out.println("--------------------------------");

                            System.out.println("Donor ID : " + rs.getInt("donor_id"));

                            System.out.println("Name : "
                                    + rs.getString("donor_name"));

                            System.out.println("Blood Group : " + rs.getString("blood_group"));

                            System.out.println("Mobile : " + rs.getString("phone_no"));

                            System.out.println("Available : " + rs.getBoolean("available"));
                        }

                        if (!cityFound) {
                            System.out.println("No Donor Found.");
                        } else {
                            LogThread t = new LogThread("Search By City : " + cityName);

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

            String check = "SELECT * FROM donor WHERE donor_id=?";

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
                        String donorName = sc.nextLine();

                        String sql1 = "UPDATE donor SET donor_name=? WHERE donor_id=?";

                        pst = con.prepareStatement(sql1);

                        pst.setString(1, donorName);

                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {
                            System.out.println("Name Updated Successfully.");

                            LogThread t = new LogThread("Updated Name of Donor ID : " + updateDonorID);

                            t.start();
                        }

                        pst.close();

                        break;

                    // UPDATE AGE
                    //-----------------------------------------

                    case 2:
                        int donorAge;

                        while (true) {
                            try {
                                System.out.println("Enter Updated Age");

                                donorAge = sc.nextInt();

                                sc.nextLine();

                                if (donorAge >= 18 &&
                                        donorAge <= 65)

                                    break;
                                else {

                                    throw new InvalidDonorException(
                                            "Age should be between 18 and 65.");
                                }

                            } catch (InputMismatchException e) {

                                System.out.println("Enter Numeric Age.");

                                sc.nextLine();
                            } catch (InvalidDonorException e) {

                                System.out.println(e.getMessage());
                            }
                        }

                        String sql2 = "UPDATE donor SET donor_age=? WHERE donor_id=?";
                        pst = con.prepareStatement(sql2);

                        pst.setInt(1, donorAge);

                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {
                            System.out.println("Age Updated Successfully.");

                            LogThread t = new LogThread("Updated Age of Donor ID : " + updateDonorID);
                            t.start();
                        }

                        pst.close();

                        break;

                    // UPDATE MOBILE

                    case 3:
                        System.out.println("Enter Updated Mobile Number");

                        String mobileNo = sc.nextLine();

                        while (true) {
                            if (mobileNo.length() != 10) {

                                System.out.println("Invalid Mobile Number");
                                mobileNo = sc.nextLine();
                            } else if (mobileNo.charAt(0) != '9' &&
                                    mobileNo.charAt(0) != '8' &&
                                    mobileNo.charAt(0) != '7' &&
                                    mobileNo.charAt(0) != '6') {

                                System.out.println("Invalid Mobile Number");

                                mobileNo = sc.nextLine();
                            } else
                                break;
                        }

                        String sql3 = "UPDATE donor SET phone_no=? WHERE donor_id=?";

                        pst = con.prepareStatement(sql3);

                        pst.setString(1, mobileNo);
                        pst.setInt(2, updateDonorID);
                        if (pst.executeUpdate() > 0) {
                            System.out.println("Mobile Updated Successfully.");

                            LogThread t = new LogThread("Updated Mobile of Donor ID : " + updateDonorID);
                            t.start();
                        }

                        pst.close();

                        break;


                    // UPDATE EMAIL

                    case 4:
                        System.out.println("Enter Updated Email");

                        String email = sc.nextLine();

                        while (true) {

                            if (email.contains("@") && email.contains("."))
                                break;

                            else {
                                System.out.println("Invalid Email.");
                                email = sc.nextLine();
                            }
                        }

                        String sql4 = "UPDATE donor SET email=? WHERE donor_id=?";

                        pst = con.prepareStatement(sql4);

                        pst.setString(1, email);
                        pst.setInt(2, updateDonorID);

                        if (pst.executeUpdate() > 0) {
                            System.out.println("Email Updated Successfully.");
                            LogThread t = new LogThread("Updated Email of Donor ID : " + updateDonorID);
                            t.start();
                        }
                        pst.close();

                        break;

                    // UPDATE CITY
                    case 5:

                        System.out.println("Enter Updated City");

                        String cityName = sc.nextLine();

                        String sql5 = "UPDATE donor SET city_name=? WHERE donor_id=?";

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

                        String sql6 = "UPDATE donor SET available=? WHERE donor_id=?";
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
            String check = "SELECT * FROM donor WHERE donor_id=?";
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
                String sql = "DELETE FROM donor WHERE donor_id=?";
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

        try {
            Connection con = DatabaseConnection.getConnection();

            String query = "SELECT donor_id, donor_name, donor_age, donor_gender, " +
                    "blood_group, city_name, phone_no, email, donor_history, available " +
                    "FROM donor";

            PreparedStatement pst = con.prepareStatement(query);
            ResultSet rs = pst.executeQuery();

            System.out.println("\n================================================================================================================");
            System.out.println("                                                   DONOR LIST");
            System.out.println("================================================================================================================");

            System.out.printf("%-8s %-18s %-5s %-10s %-8s %-15s %-15s %-25s %-18s %-10s%n",
                    "ID", "NAME", "AGE", "GENDER", "GROUP",
                    "CITY", "PHONE", "EMAIL", "HISTORY", "AVAILABLE");

            System.out.println("----------------------------------------------------------------------------------------------------------------");

            boolean found = false;

            while (rs.next()) {

                found = true;

                System.out.printf("%-8d %-18s %-5d %-10s %-8s %-15s %-15s %-25s %-18s %-10s%n",
                        rs.getInt("donor_id"),
                        rs.getString("donor_name"),
                        rs.getInt("donor_age"),
                        rs.getString("donor_gender"),
                        rs.getString("blood_group"),
                        rs.getString("city_name"),
                        rs.getString("phone_no"),
                        rs.getString("email"),
                        rs.getString("donor_history"),
                        rs.getBoolean("available"));
            }

            if (!found) {
                System.out.println("No donors found in database.");
            }

            System.out.println("================================================================================================================");

            rs.close();
            pst.close();
            con.close();

        } catch (SQLException e) {
            System.out.println("Donor Error: " + e.getMessage());
        }
    }
}

//inventory manager class

package service;

import database.DatabaseConnection;
import model.BloodInventory;
import java.sql.*;

public class InventoryManager{

    public void addInventory(BloodInventory inventory){

        try{
            Connection con=DatabaseConnection.getConnection();

            String query="INSERT INTO blood_inventory " +
                    "(inventory_id, blood_group, units_available, min_units_availability) " +
                    "VALUES (?, ?, ?, ?)";

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

    //display inventory
    public void displayInventory(){

        try{
            Connection con = DatabaseConnection.getConnection();

            String query = "SELECT inventory_id, blood_group, units_available, min_units_availability " +
                    "FROM blood_inventory";

            PreparedStatement pst = con.prepareStatement(query);
            ResultSet rs = pst.executeQuery();

            System.out.println("\n===============================================================");
            System.out.println("                       BLOOD INVENTORY");
            System.out.println("===============================================================");
            System.out.printf("%-8s %-15s %-20s %-15s%n",
                    "ID", "BLOOD GROUP", "AVAILABLE UNITS", "MINIMUM UNITS");
            System.out.println("---------------------------------------------------------------");

            while(rs.next()){
                System.out.printf("%-8d %-15s %-20d %-15d%n",
                        rs.getInt("inventory_id"),
                        rs.getString("blood_group"),
                        rs.getInt("units_available"),
                        rs.getInt("min_units_availability"));
            }

            System.out.println("===============================================================");

            rs.close();
            pst.close();
            con.close();

        }catch(SQLException e){
            System.out.println("Inventory Error: " + e.getMessage());
        }
    }

    //Search inventory
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
            Connection con= DatabaseConnection.getConnection();

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

//manageable interface

package service;

public interface Manageable{
    public void addDonor();
    public void searchDonor();
    public void updateDonor();
    void deleteDonor();
    void displayDonors();
}


//request manager class

package service;

import java.sql.*;
import java.util.Scanner;
import database.DatabaseConnection;

public class RequestManager {

    Scanner sc=new Scanner(System.in);

    InventoryManager inventoryManager=new InventoryManager();


    public void addRequest(){

        try{

            Connection con=DatabaseConnection.getConnection();

            String query="insert into blood_request values(?,?,?,?,?,?,?,?,?)";

            PreparedStatement pst=con.prepareStatement(query);


            System.out.print("Enter Request ID: ");
            int id=sc.nextInt();
            sc.nextLine();

            System.out.print("Enter Patient Name: ");
            String name = sc.nextLine();

            while (name.trim().isEmpty() || !name.matches("[a-zA-Z ]+")) {
                System.out.print("Invalid Patient Name! Enter again: ");
                name = sc.nextLine();
            }

            System.out.print("Enter Patient Age: ");
            int age = sc.nextInt();

            while (age < 1 || age > 110) {
                System.out.print("Invalid Age! Enter age between 1 and 110: ");
                age = sc.nextInt();
            }

            System.out.print("Enter Blood Group: ");
            String group = sc.next().toUpperCase();

            while (!(group.equals("A+") ||
                    group.equals("A-") ||
                    group.equals("B+") ||
                    group.equals("B-") ||
                    group.equals("AB+") ||
                    group.equals("AB-") ||
                    group.equals("O+") ||
                    group.equals("O-"))) {

                System.out.print("Invalid Blood Group! Enter again: ");
                group = sc.next().toUpperCase();
            }

            System.out.print("Enter Required Units: ");
            int units = sc.nextInt();

            while (units < 1 || units > 10) {
                System.out.print("Units should be between 1 and 10. Enter again: ");
                units = sc.nextInt();
            }
            sc.nextLine();
            System.out.print("Enter Hospital Name: ");
            String hospital = sc.nextLine();

            boolean validHospital = false;

            while (!validHospital){

                if (!hospital.trim().isEmpty()) {
                    validHospital = true;

                    for (int i = 0; i < hospital.length(); i++) {
                        char ch = hospital.charAt(i);

                        if (!Character.isLetter(ch) && ch != ' ') {
                            validHospital = false;
                            break;
                        }
                    }
                }

                if (!validHospital) {
                    System.out.print("Invalid Hospital Name! Enter letters only: ");
                    hospital = sc.nextLine();
                }
            }

            System.out.print("Enter City: ");
            String city = sc.nextLine();

            while (city.trim().isEmpty()) {
                System.out.print("City cannot be empty. Enter again: ");
                city = sc.nextLine();
            }

            System.out.print("Enter Contact Number: ");
            String contact = sc.nextLine();

            boolean valid = false;

            while (!valid) {

                if (contact.length() == 10 && (contact.charAt(0) == '6' ||
                                contact.charAt(0) == '7' ||
                                contact.charAt(0) == '8' ||
                                contact.charAt(0) == '9')) {

                    valid = true;

                    for (int i = 0; i < contact.length(); i++) {

                        if (!Character.isDigit(contact.charAt(i))) {
                            valid = false;
                            break;
                        }
                    }
                }

                if (!valid){
                    System.out.print("Invalid Contact Number! Enter a valid 10-digit number starting with 6, 7, 8 or 9: ");
                    contact = sc.nextLine();
                }
            }


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
            Connection con = DatabaseConnection.getConnection();

            String query = "SELECT request_id, patient_name, patient_age, blood_group, " +
                    "units_required, hospital_name, city, contact, request_status " +
                    "FROM blood_request";

            PreparedStatement pst = con.prepareStatement(query);
            ResultSet rs = pst.executeQuery();

            System.out.println("\n================================================================================================================");
            System.out.println("                                           BLOOD REQUESTS");
            System.out.println("================================================================================================================");
            System.out.printf("%-7s %-18s %-5s %-8s %-6s %-22s %-13s %-13s %-12s%n",
                    "ID", "PATIENT", "AGE", "GROUP", "UNITS",
                    "HOSPITAL", "CITY", "CONTACT", "STATUS");
            System.out.println("----------------------------------------------------------------------------------------------------------------");

            while(rs.next()){

                System.out.printf("%-7d %-18s %-5d %-8s %-6d %-22s %-13s %-13s %-12s%n",
                        rs.getInt("request_id"),
                        rs.getString("patient_name"),
                        rs.getInt("patient_age"),
                        rs.getString("blood_group"),
                        rs.getInt("units_required"),
                        rs.getString("hospital_name"),
                        rs.getString("city"),
                        rs.getString("contact"),
                        rs.getString("request_status"));
            }
            System.out.println("================================================================================================================");

            rs.close();
            pst.close();
            con.close();

        }catch(SQLException e){
            System.out.println("Request Error: " + e.getMessage());
        }
    }
    public void updateRequest(){

        try{
            Connection con = DatabaseConnection.getConnection();

            System.out.print("Enter Request ID: ");
            int id = sc.nextInt();

            String check = "SELECT request_status FROM blood_request WHERE request_id=?";

            PreparedStatement checkStmt = con.prepareStatement(check);

            checkStmt.setInt(1, id);

            ResultSet rs = checkStmt.executeQuery();

            if(rs.next()){

                String currentStatus = rs.getString("request_status");

                System.out.println("Current Status: " + currentStatus);

                System.out.println("1. Processing");
                System.out.println("2. Fulfilled");

                System.out.print("Enter New Status: ");
                int choice = sc.nextInt();

                String status;

                if(choice == 1){
                    status = "Processing";
                }
                else if(choice == 2){
                    status = "Fulfilled";
                }
                else{
                    System.out.println("Invalid Status Choice");

                    rs.close();
                    checkStmt.close();
                    con.close();

                    return;
                }


                // CALL PROCEDURE

                CallableStatement cs = con.prepareCall("{call process_blood_request(?, ?)}");

                cs.setInt(1, id);
                cs.setString(2, status);

                cs.execute();

                System.out.println("Request Updated Successfully");

                cs.close();

            }
            else{
                System.out.println("Request Not Found");
            }

            rs.close();
            checkStmt.close();
            con.close();

        }
        catch(SQLException e){
            System.out.println("Request Error: " + e.getMessage());
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
        }
        catch(SQLException e){
            System.out.println(e);
        }
    }
}


//user manager class

package service;

// USER MANAGER CLASS

import model.User;
import database.DatabaseConnection;

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


    // =========================================================
    // ADD USER - DS
    // =========================================================

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


    // =========================================================
    // CHECK USERNAME
    // =========================================================

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


    // =========================================================
    // SEARCH BY ID
    // =========================================================

    public User searchById(int id) {

        for (User user : users) {

            if (user.getUserId() == id)
                return user;
        }

        return null;
    }


    // =========================================================
    // SEARCH BY USERNAME
    // =========================================================

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


    // =========================================================
    // UPDATE USER - ARRAYLIST
    // =========================================================

    public boolean updateUser(User updatedUser) {

        if (updatedUser == null)
            return false;

        User existingUser =
                searchById(updatedUser.getUserId());

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

        // ROLE
        existingUser.setRole(updatedUser.getRole());

        return true;
    }


    // =========================================================
    // DELETE USER - ARRAYLIST
    // =========================================================

    public boolean deleteUser(int id) {

        User user = searchById(id);

        if (user == null)
            return false;

        users.remove(user);

        return true;
    }


    // =========================================================
    // TOTAL USERS
    // =========================================================

    public int getTotalUsers() {

        return users.size();
    }


    // =========================================================
    // DISPLAY ALL USERS
    // =========================================================

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


    // =========================================================
    // DATABASE / JDBC METHODS
    // =========================================================


    // =========================================================
    // SAVE USER TO DATABASE
    // =========================================================

    public boolean saveUserToDB(User user) throws Exception {

        if (user == null)
            return false;

        String sql =
                "INSERT INTO users " +
                        "(user_id, name, age, gender, blood_group, phone, " +
                        "email, address, username, password, " +
                        "last_donation_date, role) " +
                        "VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)";

        try (Connection con =
                     DatabaseConnection.getConnection();

             PreparedStatement pst =
                     con.prepareStatement(sql)) {

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
            pst.setString(12, user.getRole());

            int rows = pst.executeUpdate();

            return rows > 0;
        }
    }


    // =========================================================
    // LOAD USERS FROM DATABASE
    // =========================================================

    public void loadUsersFromDB() throws Exception {

        String sql = "SELECT * FROM users";

        try (Connection con =
                     DatabaseConnection.getConnection();

             PreparedStatement pst =
                     con.prepareStatement(sql);

             ResultSet rs =
                     pst.executeQuery()) {

            users.clear();

            while (rs.next()) {

                User user = new User();

                user.setUserId(
                        rs.getInt("user_id")
                );

                user.setName(
                        rs.getString("name")
                );

                user.setAge(
                        rs.getInt("age")
                );

                user.setGender(
                        rs.getString("gender")
                );

                user.setBloodGroup(
                        rs.getString("blood_group")
                );

                user.setPhone(
                        rs.getString("phone")
                );

                user.setEmail(
                        rs.getString("email")
                );

                user.setAddress(
                        rs.getString("address")
                );

                user.setUsername(
                        rs.getString("username")
                );

                user.setPassword(
                        rs.getString("password")
                );

                user.setLastDonationDate(
                        rs.getString("last_donation_date")
                );

                // ROLE
                user.setRole(
                        rs.getString("role")
                );

                users.add(user);


                // UPDATE NEXT USER ID

                if (user.getUserId() >= nextUserId) {

                    nextUserId =
                            user.getUserId() + 1;
                }
            }
        }
    }


    // =========================================================
    // UPDATE USER IN DATABASE
    // =========================================================

    public boolean updateUserInDB(User user) throws Exception {

        if (user == null)
            return false;

        String sql =
                "UPDATE users SET " +
                        "name=?, age=?, gender=?, blood_group=?, phone=?, " +
                        "email=?, address=?, username=?, password=?, " +
                        "last_donation_date=?, role=? " +
                        "WHERE user_id=?";

        try (Connection con =
                     DatabaseConnection.getConnection();

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

            // ROLE
            pst.setString(11, user.getRole());

            pst.setInt(12, user.getUserId());

            int rows = pst.executeUpdate();

            return rows > 0;
        }
    }


    // =========================================================
    // DELETE USER FROM DATABASE
    // =========================================================

    public boolean deleteUserFromDB(int id) throws Exception {

        String sql =
                "DELETE FROM users WHERE user_id=?";

        try (Connection con =
                     DatabaseConnection.getConnection();

             PreparedStatement pst =
                     con.prepareStatement(sql)) {

            pst.setInt(1, id);

            int rows =
                    pst.executeUpdate();

            return rows > 0;
        }
    }


    // =========================================================
    // LOGIN CHECK - ARRAYLIST
    // =========================================================

    public User loginUser(
            String username,
            String password) {

        for (User user : users) {

            if (user.getUsername() != null &&
                    user.getPassword() != null &&
                    user.getUsername()
                            .equalsIgnoreCase(username) &&
                    user.getPassword()
                            .equals(password)) {

                return user;
            }
        }

        return null;
    }


    // =========================================================
    // LOGIN CHECK - DATABASE
    // =========================================================

    public User loginUserFromDB(
            String username,
            String password) throws Exception {

        String sql =
                "SELECT * FROM users " +
                        "WHERE username=? AND password=?";

        try (Connection con =
                     DatabaseConnection.getConnection();

             PreparedStatement pst =
                     con.prepareStatement(sql)) {

            pst.setString(1, username);
            pst.setString(2, password);

            try (ResultSet rs =
                         pst.executeQuery()) {

                if (rs.next()) {

                    User user = new User();

                    user.setUserId(
                            rs.getInt("user_id")
                    );

                    user.setName(
                            rs.getString("name")
                    );

                    user.setAge(
                            rs.getInt("age")
                    );

                    user.setGender(
                            rs.getString("gender")
                    );

                    user.setBloodGroup(
                            rs.getString("blood_group")
                    );

                    user.setPhone(
                            rs.getString("phone")
                    );

                    user.setEmail(
                            rs.getString("email")
                    );

                    user.setAddress(
                            rs.getString("address")
                    );

                    user.setUsername(
                            rs.getString("username")
                    );

                    user.setPassword(
                            rs.getString("password"));

                    user.setLastDonationDate(rs.getString("last_donation_date"));

                    // ROLE
                    user.setRole(
                            rs.getString("role"));
                    return user;
                }
            }
        }
        return null;
    }
}

// admin menu class

import java.util.Scanner;

import service.DonorManager;
import service.InventoryManager;
import service.RequestManager;

public class AdminMenu {

    Scanner sc = new Scanner(System.in);

    DonorManager donorManager = new DonorManager();
    RequestManager requestManager = new RequestManager();
    InventoryManager inventoryManager = new InventoryManager();

    public void showAdminMenu() {

        int choice;

        do {
            System.out.println("\n===== ADMIN MENU =====");
            System.out.println("1. Manage Donors");
            System.out.println("2. Manage Blood Requests");
            System.out.println("3. Manage Blood Inventory");
            System.out.println("4. Logout");

            System.out.print("Enter choice: ");
            choice = sc.nextInt();

            switch (choice) {

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

        } while (choice != 4);
    }


    // ================= DONOR MENU =================

    public void donorMenu() {

        int choice;

        do {
            System.out.println("\n===== DONOR MANAGEMENT =====");
            System.out.println("1. Add Donor");
            System.out.println("2. Display Donors");
            System.out.println("3. Search Donor");
            System.out.println("4. Update Donor");
            System.out.println("5. Delete Donor");
            System.out.println("6. Back");

            System.out.print("Enter choice: ");
            choice = sc.nextInt();

            switch (choice) {

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
                    donorManager.updateDonor();
                    break;

                case 5:
                    donorManager.deleteDonor();
                    break;

                case 6:
                    System.out.println("BACK");
                    break;

                default:
                    System.out.println("Invalid Choice");
            }

        } while (choice != 6);
    }


    // ================= REQUEST MENU =================

    public void requestMenu() {

        int choice;

        do {
            System.out.println("\n===== REQUEST MANAGEMENT =====");
            System.out.println("1. Add Blood Request");
            System.out.println("2. Display Requests");
            System.out.println("3. Search Blood Request");
            System.out.println("4. Update Request Status");
            System.out.println("5. Back");

            System.out.print("Enter choice: ");
            choice = sc.nextInt();

            switch (choice) {

                case 1:
                    requestManager.addRequest();
                    break;

                case 2:
                    requestManager.displayRequests();
                    break;

                case 3:
                    requestManager.searchRequest();
                    break;

                case 4:
                    requestManager.updateRequest();
                    break;

                case 5:
                    System.out.println("BACK");
                    break;

                default:
                    System.out.println("Invalid Choice");
            }

        } while (choice != 5);
    }


    // ================= INVENTORY MENU =================

    public void inventoryMenu() {

        int choice;

        do {
            System.out.println("\n===== INVENTORY MANAGEMENT =====");
            System.out.println("1. Display Inventory");
            System.out.println("2. Search Blood Stock");
            System.out.println("3. Update Inventory");
            System.out.println("4. Delete Inventory");
            System.out.println("5. Check Blood Availability");
            System.out.println("6. Back");

            System.out.print("Enter choice: ");
            choice = sc.nextInt();

            switch (choice) {

                case 1:
                    inventoryManager.displayInventory();
                    break;

                case 2:
                    System.out.print("Enter Blood Group: ");
                    String group = sc.next();
                    inventoryManager.searchInventory(group);
                    break;

                case 3:
                    System.out.print("Enter Blood Group: ");
                    String bg = sc.next();

                    System.out.print("Enter New Units: ");
                    int units = sc.nextInt();

                    inventoryManager.updateInventory(bg, units);
                    break;

                case 4:
                    System.out.print("Enter Inventory ID: ");
                    int id = sc.nextInt();

                    inventoryManager.deleteInventory(id);
                    break;

                case 5:
                    System.out.print("Enter Blood Group: ");
                    String blood = sc.next();

                    System.out.print("Enter Required Units: ");
                    int required = sc.nextInt();

                    boolean result =
                            inventoryManager.checkAvailability(blood, required);

                    if (result)
                        System.out.println("Blood Available");
                    else
                        System.out.println("Blood Not Available");

                    break;

                case 6:
                    System.out.println("BACK");
                    break;

                default:
                    System.out.println("Invalid Choice");
            }

        } while (choice != 6);
    }
}


//MAIN CLASS =================================================

import database.DatabaseConnection;
import model.User;
import model.Admin;
import service.DonorManager;
import service.InventoryManager;
import service.RequestManager;
import service.UserManager;

import java.sql.Connection;
import java.sql.SQLException;
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeParseException;
import java.util.Scanner;

public class BloodDonorFinder {

    static Scanner sc = new Scanner(System.in);

    static UserManager userManager = new UserManager();
    static DonorManager donorManager = new DonorManager();
    static InventoryManager inventoryManager = new InventoryManager();
    static RequestManager requestManager = new RequestManager();

    static Admin admin;

    // DATE FORMAT
    static DateTimeFormatter dateFormatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");

    public static void main(String[] args) {

        System.out.println("==============================================");
        System.out.println("        lifelink1 - BLOOD DONOR FINDER");
        System.out.println("==============================================");

        // DATABASE CONNECTION
        try {
            Connection con = DatabaseConnection.getConnection();

            if (con != null) {
                System.out.println("Database connected successfully.");
                DatabaseConnection.closeConnection(con);
            }

            // Load existing users
            userManager.loadUsersFromDB();

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

                case 1:
                    registerUser();
                    break;

                case 2:
                    userLogin();
                    break;

                case 3:
                    adminLogin();
                    break;

                case 4:

                    System.out.println("\nThank you for using lifelink1.");

                    System.out.println("Application closed successfully.");

                    break;

                default:

                    System.out.println("Invalid choice. Please try again.");
            }

        } while (choice != 4);

        sc.close();
    }


    // =========================================================
    // USER REGISTRATION
    // =========================================================

    public static void registerUser() {

        System.out.println("\n==============================================");
        System.out.println("              USER REGISTRATION");
        System.out.println("==============================================");

        User user = new User();


        // -----------------------------------------------------
        // NAME
        // -----------------------------------------------------

        String name;

        while (true) {

            System.out.print("Enter Name: ");
            name = sc.nextLine();

            boolean valid = true;

            if (name.trim().isEmpty()) {
                valid = false;
            }

            for (int i = 0; i < name.length(); i++) {

                char ch = name.charAt(i);

                if (!Character.isLetter(ch) && ch != ' ') {
                    valid = false;
                    break;
                }
            }

            if (valid) {
                break;
            }
            System.out.println("Invalid name. Enter letters and space only.");
        }
        user.setName(name);

        // AGE
        int age;

        while (true) {

            System.out.print("Enter Age: ");

            try {
                age = sc.nextInt();
                sc.nextLine();

                if (age >= 18 && age <= 65) {
                    break;
                }
                System.out.println("Age must be between 18 and 65.");

            } catch (Exception e) {
                System.out.println("Invalid age. Enter a number.");
                sc.nextLine();
            }
        }
        user.setAge(age);

        // GENDER
        String gender;

        while (true) {

            System.out.print("Enter Gender (Male/Female/Other): ");

            gender = sc.nextLine();

            if (gender.equalsIgnoreCase("Male") ||
                    gender.equalsIgnoreCase("Female") ||
                    gender.equalsIgnoreCase("Other")) {

                break;
            }
            System.out.println("Invalid gender. Enter Male, Female or Other.");
        }
        user.setGender(gender);

        // BLOOD GROUP
        String bloodGroup;
        while (true) {

            System.out.print("Enter Blood Group: ");

            bloodGroup = sc.nextLine().toUpperCase();

            if (bloodGroup.equals("A+") ||
                    bloodGroup.equals("A-") ||
                    bloodGroup.equals("B+") ||
                    bloodGroup.equals("B-") ||
                    bloodGroup.equals("AB+") ||
                    bloodGroup.equals("AB-") ||
                    bloodGroup.equals("O+") ||
                    bloodGroup.equals("O-")) {

                break;
            }
            System.out.println("Invalid blood group.");
        }
        user.setBloodGroup(bloodGroup);

        // ROLE
        String role;

        while (true) {
            System.out.print("Register as Donor or Receiver: ");

            role = sc.nextLine().trim();

            if (role.equalsIgnoreCase("Donor")) {
                role = "Donor";
                break;
            } else if (role.equalsIgnoreCase("Receiver")) {
                role = "Receiver";
                break;

            } else {
                System.out.println("Invalid role. Please enter Donor or Receiver.");
            }
        }
        user.setRole(role);

        // PHONE
        String phone;

        while (true) {

            System.out.print("Enter Phone Number: ");

            phone = sc.nextLine();

            boolean valid = true;

            if (phone.length() != 10) {
                valid = false;
            }

            for (int i = 0; i < phone.length(); i++) {

                if (!Character.isDigit(phone.charAt(i))) {

                    valid = false;
                    break;
                }
            }

            if (valid && (phone.charAt(0) == '6' ||
                            phone.charAt(0) == '7' ||
                            phone.charAt(0) == '8' ||
                            phone.charAt(0) == '9')) {

                break;
            }
            System.out.println("Invalid phone number.");
        }
        user.setPhone(phone);

        // EMAIL
        String email;

        while (true) {

            System.out.print("Enter Email: ");
            email = sc.nextLine().trim();

            int atPosition = email.indexOf("@");
            int lastAtPosition = email.lastIndexOf("@");
            int dotPosition = email.lastIndexOf(".");

            boolean valid = true;

            if (!email.equals(email.toLowerCase())) {
                valid = false;
            }

            if (email.contains(" ")) {
                valid = false;
            }

            if (atPosition <= 0 || atPosition != lastAtPosition) {
                valid = false;
            }

            if (dotPosition <= atPosition + 1 || dotPosition == email.length() - 1) {
                valid = false;
            }

            if (!valid) {
                System.out.println("Invalid email format. Please enter a valid lowercase email.");
            } else {
                break;
            }
        }
        user.setEmail(email);

        // ADDRESS
        String address;

        while (true) {

            System.out.print("Enter Address: ");

            address = sc.nextLine();

            if (!address.trim().isEmpty()) {
                break;
            }
            System.out.println("Address cannot be empty.");
        }
        user.setAddress(address);

        // USERNAME
        String username;

        while (true) {

            System.out.print("Enter Username: ");

            username = sc.nextLine();

            if (username.trim().isEmpty()) {

                System.out.println("Username cannot be empty.");

            } else if (userManager.isUsernameExists(username)) {

                System.out.println("Username already exists.");

            } else {

                break;
            }
        }
        user.setUsername(username);


        // PASSWORD
        String password;

        while (true) {

            System.out.print("Enter Password: ");
            password = sc.nextLine();

            if (password.length() >= 6) {
                break;
            }
            System.out.println("Password must be at least 6 characters.");
        }
        user.setPassword(password);


        // LAST DONATION DATE
        // ONLY FOR DONOR

        if (role.equalsIgnoreCase("Donor")) {

            String date;

            while (true) {

                System.out.print("Enter Last Donation Date (dd/MM/yyyy): ");
                date = sc.nextLine();

                try {

                    LocalDate donationDate = LocalDate.parse(date, dateFormatter);

                    int day = Integer.parseInt(date.substring(0, 2));
                    int month = Integer.parseInt(date.substring(3, 5));
                    int year = Integer.parseInt(date.substring(6, 10));

                    if (donationDate.getDayOfMonth() != day ||
                            donationDate.getMonthValue() != month ||
                            donationDate.getYear() != year) {

                        System.out.println("Invalid date. Please enter a valid date.");
                        continue;
                    }

                    LocalDateTime currentDateTime = LocalDateTime.now();
                    LocalDate today = currentDateTime.toLocalDate();

                    if (donationDate.isAfter(today)) {

                        System.out.println("Donation date cannot be in the future.");
                        continue;
                    }

                    LocalDate twoYearsAgo = today.minusYears(2);

                    if (!donationDate.isBefore(twoYearsAgo)) {
                        break;
                    }

                    System.out.println("Donation date must be within the last two years.");

                } catch (DateTimeParseException e) {

                    System.out.println("Invalid date. Use dd/MM/yyyy.");

                } catch (Exception e) {
                    System.out.println("Invalid date. Please enter a valid date.");
                }
            }
            user.setLastDonationDate(date);

        } else {
            user.setLastDonationDate(null);
        }

        // GENERATE USER ID
        user.setUserId(userManager.generateUserId());

        // ADD USER
        boolean added = userManager.addUser(user);

        if (added) {

            System.out.println("\nUser registered successfully.");

            System.out.println("Your User ID is: " + user.getUserId());

            System.out.println("Role: " + user.getRole());


            // SAVE USER TO DATABASE
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


    // =========================================================
    // USER LOGIN
    // =========================================================

    public static void userLogin() {

        System.out.println("\n==============================================");
        System.out.println("                 USER LOGIN");
        System.out.println("==============================================");

        System.out.print("Enter Username: ");
        String username = sc.nextLine();

        System.out.print("Enter Password: ");
        String password = sc.nextLine();


        User user = userManager.loginUser(username, password);


        // If not found in ArrayList, check database

        if (user == null) {

            try {

                user = userManager.loginUserFromDB(username, password);

            } catch (Exception e) {
                System.out.println("Database Error: " + e.getMessage());
            }
        }

        // LOGIN RESULT

        if (user != null) {

            System.out.println("\nLogin Successful.");

            System.out.println("Welcome, " + user.getName() + "!");

            System.out.println("Role: " + user.getRole());


            // ROLE BASED MENU

            if (user.getRole() != null && user.getRole().equalsIgnoreCase("Donor")) {

                donorUserMenu(user);

            } else if (user.getRole() != null &&
                    user.getRole().equalsIgnoreCase("Receiver")) {

                receiverUserMenu(user);

            } else {
                System.out.println("Invalid user role.");
            }

        } else {
            System.out.println("Invalid Username or Password.");
        }
    }


    // =========================================================
    // DONOR MENU
    // =========================================================

    public static void donorUserMenu(User user) {

        int choice;

        do {

            System.out.println("\n==============================================");
            System.out.println("                 DONOR MENU");
            System.out.println("==============================================");

            System.out.println("1. View My Profile");
            System.out.println("2. Update My Profile");
            System.out.println("3. Check Donation Eligibility");
            System.out.println("4. Logout");

            System.out.print("Enter choice: ");

            try {
                choice = sc.nextInt();
                sc.nextLine();

            } catch (Exception e) {
                System.out.println("Invalid input. Enter a number.");

                sc.nextLine();
                choice = 0;
            }

            switch (choice) {
                case 1:
                    viewMyProfile(user);
                    break;

                case 2:
                    updateMyProfile(user);
                    break;

                case 3:
                    checkDonationEligibility(user);
                    break;

                case 4:
                    System.out.println("Donor logged out successfully.");
                    break;

                default:
                    System.out.println("Invalid choice.");
            }
        } while (choice != 4);
    }

    // RECEIVER MENU

    public static void receiverUserMenu(User user) {

        int choice;

        do {
            System.out.println("\n==============================================");
            System.out.println("                RECEIVER MENU");
            System.out.println("==============================================");

            System.out.println("1. Create Blood Request");
            System.out.println("2. View My Request Status");
            System.out.println("3. Logout");

            System.out.print("Enter choice: ");

            try {

                choice = sc.nextInt();
                sc.nextLine();

            } catch (Exception e) {

                System.out.println("Invalid input. Enter a number.");
                sc.nextLine();
                choice = 0;
            }

            switch (choice) {

                case 1:
                    createBloodRequest(user);
                    break;

                case 2:
                    viewMyRequestStatus(user);
                    break;

                case 3:
                    System.out.println("Receiver logged out successfully.");
                    break;

                default:
                    System.out.println("Invalid choice.");
            }

        } while (choice != 3);
    }

    public static void createBloodRequest(User user) {

        System.out.println("\n==============================================");
        System.out.println("             CREATE BLOOD REQUEST");
        System.out.println("==============================================");

        System.out.println("1. Blood Required For Myself");
        System.out.println("2. Blood Required For Someone Else");

        System.out.print("Enter choice: ");
        int choice = sc.nextInt();
        sc.nextLine();

        if (choice != 1 && choice != 2) {
            System.out.println("Invalid choice.");
            return;
        }

        try {

            Connection con = DatabaseConnection.getConnection();

            String query = "INSERT INTO blood_request " +
                            "(request_id, patient_name, patient_age, blood_group, " +
                            "units_required, hospital_name, city, contact, request_status) " +
                            "VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)";

            java.sql.PreparedStatement pst = con.prepareStatement(query);

            // REQUEST ID

            System.out.print("Enter Request ID: ");
            int requestId = sc.nextInt();
            sc.nextLine();


            String patientName;
            int patientAge;
            String bloodGroup;


            // FOR MYSELF
            if (choice == 1) {

                patientName = user.getName();
                patientAge = user.getAge();
                bloodGroup = user.getBloodGroup();

                System.out.println("Patient Name: " + patientName);

                System.out.println("Patient Age: " + patientAge);

                System.out.println("Blood Group: " + bloodGroup);

            }

            // FOR SOMEONE ELSE
            else {
                while (true) {

                    System.out.print("Enter Patient Name: ");
                    patientName = sc.nextLine();

                    boolean valid = true;

                    if (patientName.trim().isEmpty()) {
                        valid = false;
                    }

                    for (int i = 0; i < patientName.length(); i++) {
                        char ch = patientName.charAt(i);

                        if (!Character.isLetter(ch) && ch != ' ') {
                            valid = false;
                            break;
                        }
                    }

                    if (valid) {
                        break;
                    }
                    System.out.println("Invalid Patient Name! Enter letters only.");
                }


                System.out.print("Enter Patient Age: ");
                patientAge = sc.nextInt();

                while (patientAge < 1 || patientAge > 110) {
                    System.out.print("Invalid Age! Enter age between 1 and 110: ");

                    patientAge = sc.nextInt();
                }

                sc.nextLine();

                System.out.print("Enter Blood Group: ");
                bloodGroup = sc.nextLine().toUpperCase();


                while (!(bloodGroup.equals("A+") ||
                        bloodGroup.equals("A-") ||
                        bloodGroup.equals("B+") ||
                        bloodGroup.equals("B-") ||
                        bloodGroup.equals("AB+") ||
                        bloodGroup.equals("AB-") ||
                        bloodGroup.equals("O+") ||
                        bloodGroup.equals("O-"))) {

                    System.out.print("Invalid Blood Group! Enter again: ");

                    bloodGroup = sc.nextLine().toUpperCase();
                }
            }
            // REQUIRED UNITS

            System.out.print("Enter Required Units: ");

            int units = sc.nextInt();

            while (units < 1 || units > 10) {
                System.out.print("Units should be between 1 and 10. Enter again: ");
                units = sc.nextInt();
            }
            sc.nextLine();

            // HOSPITAL

            System.out.print("Enter Hospital Name: ");

            String hospital = sc.nextLine();

            while (hospital.trim().isEmpty()) {

                System.out.print("Hospital Name cannot be empty. Enter again: ");
                hospital = sc.nextLine();
            }

            // CITY

            System.out.print("Enter City: ");
            String city = sc.nextLine();

            while (city.trim().isEmpty()) {
                System.out.print("City cannot be empty. Enter again: ");
                city = sc.nextLine();
            }

            // CONTACT
            String contact;

            if (choice == 1) {

                contact = user.getPhone();

                System.out.println("Contact Number: " + contact);

            } else {
                System.out.print("Enter Contact Number: ");

                contact = sc.nextLine();

                boolean valid = false;

                while (!valid) {
                    if (contact.length() == 10 && (contact.charAt(0) == '6' ||
                                    contact.charAt(0) == '7' ||
                                    contact.charAt(0) == '8' ||
                                    contact.charAt(0) == '9')) {

                        valid = true;

                        for (int i = 0; i < contact.length(); i++) {

                            if (!Character.isDigit(contact.charAt(i))) {

                                valid = false;
                                break;
                            }
                        }
                    }

                    if (!valid) {
                        System.out.print("Invalid Contact Number! " + "Enter valid 10-digit number: ");
                        contact = sc.nextLine();
                    }
                }
            }


            // --------------------------------------------------
            // INSERT DATA
            // --------------------------------------------------

            pst.setInt(1, requestId);
            pst.setString(2, patientName);
            pst.setInt(3, patientAge);
            pst.setString(4, bloodGroup);
            pst.setInt(5, units);
            pst.setString(6, hospital);
            pst.setString(7, city);
            pst.setString(8, contact);

            // Always starts with Pending

            pst.setString(9, "Pending");


            int result = pst.executeUpdate();


            if (result > 0) {
                System.out.println("\nBlood Request Created Successfully.");
                System.out.println("Request Status: Pending");
            }
            pst.close();
            con.close();

        } catch (SQLException e) {
            System.out.println("Database Error: " + e.getMessage());
        }
    }

    // =========================================================
    // VIEW MY PROFILE
    // =========================================================

    public static void viewMyProfile(User user) {

        System.out.println("\n==============================================");
        System.out.println("                 MY PROFILE");
        System.out.println("==============================================");

        System.out.println("User ID       : " + user.getUserId());
        System.out.println("Name          : " + user.getName());
        System.out.println("Age           : " + user.getAge());
        System.out.println("Gender        : " + user.getGender());
        System.out.println("Blood Group   : " + user.getBloodGroup());
        System.out.println("Phone         : " + user.getPhone());
        System.out.println("Email         : " + user.getEmail());
        System.out.println("Address       : " + user.getAddress());
        System.out.println("Username      : " + user.getUsername());
        System.out.println("Role          : " + user.getRole());
        System.out.println("Last Donation : " + user.getLastDonationDate());
    }

    public static void viewMyRequestStatus(User user) {

        System.out.println("\n==============================================");
        System.out.println("             MY REQUEST STATUS");
        System.out.println("==============================================");

        try {
            Connection con = DatabaseConnection.getConnection();

            String query =
                    "SELECT request_id, patient_name, blood_group, " +
                            "units_required, hospital_name, request_status " +
                            "FROM blood_request WHERE contact=?";

            java.sql.PreparedStatement pst = con.prepareStatement(query);

            pst.setString(1, user.getPhone());

            java.sql.ResultSet rs = pst.executeQuery();

            boolean found = false;

            while (rs.next()) {

                found = true;

                System.out.println("----------------------------------------------");
                System.out.println("Request ID      : " + rs.getInt("request_id"));

                System.out.println("Patient Name    : " + rs.getString("patient_name"));

                System.out.println("Blood Group     : " + rs.getString("blood_group"));

                System.out.println("Units Required  : " + rs.getInt("units_required"));

                System.out.println("Hospital        : " + rs.getString("hospital_name"));

                System.out.println("Request Status  : " + rs.getString("request_status"));

                System.out.println("----------------------------------------------");
            }

            if (!found) {
                System.out.println("No blood request found for your account.");
            }

            rs.close();
            pst.close();
            con.close();

        } catch (Exception e) {
            System.out.println("Database Error: " + e.getMessage());
        }
    }


    // =========================================================
    // UPDATE MY PROFILE
    // =========================================================

    public static void updateMyProfile(User user) {

        System.out.println("\n==============================================");
        System.out.println("              UPDATE MY PROFILE");
        System.out.println("==============================================");

        System.out.println("1. Update Phone");
        System.out.println("2. Update Email");
        System.out.println("3. Update Address");
        System.out.println("4. Update Password");
        System.out.println("5. Back");

        System.out.print("Enter choice: ");

        int choice;

        try {

            choice = sc.nextInt();
            sc.nextLine();

        } catch (Exception e) {

            System.out.println("Invalid input.");
            sc.nextLine();
            return;
        }


        switch (choice) {

            case 1:

                String phone;

                while (true) {

                    System.out.print("Enter New Phone Number: ");

                    phone = sc.nextLine();

                    boolean valid = true;

                    if (phone.length() != 10) {
                        valid = false;
                    }

                    for (int i = 0; i < phone.length(); i++) {

                        if (!Character.isDigit(phone.charAt(i))) {
                            valid = false;
                            break;
                        }
                    }

                    if (valid &&
                            (phone.charAt(0) == '6' ||
                                    phone.charAt(0) == '7' ||
                                    phone.charAt(0) == '8' ||
                                    phone.charAt(0) == '9')) {

                        break;
                    }
                    System.out.println("Invalid phone number.");
                }

                user.setPhone(phone);

                break;


            case 2:

                String email;

                while (true) {

                    System.out.print("Enter New Email: ");

                    email = sc.nextLine().trim();

                    if (!email.contains("@")) {

                        System.out.println("Invalid email. Email must contain @.");
                        continue;
                    }

                    if (!email.contains(".")) {

                        System.out.println("Invalid email. Email must contain .");
                        continue;
                    }

                    if (email.toLowerCase().endsWith("@gmail")) {
                        email = email + ".com";
                    }

                    if (email.indexOf("@") > 0 &&
                            email.indexOf(".") > email.indexOf("@") + 1 &&
                            email.indexOf("@") == email.lastIndexOf("@")) {

                        break;
                    }

                    System.out.println("Invalid email format.");
                }
                user.setEmail(email);
                break;
            case 3:
                System.out.print("Enter New Address: ");

                String address = sc.nextLine();

                if (!address.trim().isEmpty()) {
                    user.setAddress(address);

                } else {
                    System.out.println("Address cannot be empty.");
                }

                break;


            case 4:
                String password;

                while (true) {
                    System.out.print("Enter New Password: ");

                    password = sc.nextLine();

                    if (password.length() >= 6) {
                        break;
                    }

                    System.out.println("Password must be at least 6 characters.");
                }
                user.setPassword(password);
                break;
            case 5:
                System.out.println("Back to Donor Menu.");
                return;
            default:
                System.out.println("Invalid choice.");
                return;
        }


        // Save updated profile

        try {

            boolean updated = userManager.updateUser(user);
            if (updated) {
                System.out.println("Profile updated successfully.");

            } else {
                System.out.println("Profile update failed.");
            }

        } catch (Exception e) {
            System.out.println("Database Error: " + e.getMessage());
        }
    }


    // =========================================================
    // DONATION ELIGIBILITY
    // =========================================================

    public static void checkDonationEligibility(User user) {

        if (user == null) {

            System.out.println(
                    "User information not available."
            );

            return;
        }


        String lastDonationDate =
                user.getLastDonationDate();

        if (lastDonationDate == null ||
                lastDonationDate.trim().isEmpty()) {

            System.out.println(
                    "Last donation date is not available."
            );

            return;
        }


        try {

            LocalDate lastDonation =
                    LocalDate.parse(
                            lastDonationDate,
                            dateFormatter
                    );

            LocalDate today =
                    LocalDate.now();


            // Male = 90 days
            // Female/Other = 120 days

            int requiredDays;

            if (user.getGender().equalsIgnoreCase("Male")) {

                requiredDays = 90;

            } else {

                requiredDays = 120;
            }


            // Calculate days manually
            // without ChronoUnit

            LocalDate checkDate = lastDonation;

            int daysPassed = 0;

            while (checkDate.isBefore(today)) {

                checkDate = checkDate.plusDays(1);
                daysPassed++;
            }


            System.out.println(
                    "\nLast Donation Date: "
                            + lastDonationDate
            );

            System.out.println(
                    "Days Since Last Donation: "
                            + daysPassed
            );

            System.out.println(
                    "Required Waiting Period: "
                            + requiredDays + " days"
            );


            if (daysPassed >= requiredDays) {

                System.out.println(
                        "You are ELIGIBLE to donate blood."
                );

            } else {

                int remainingDays =
                        requiredDays - daysPassed;

                System.out.println(
                        "You are NOT ELIGIBLE to donate yet."
                );

                System.out.println(
                        "Please wait "
                                + remainingDays
                                + " more day(s)."
                );
            }

        } catch (DateTimeParseException e) {

            System.out.println(
                    "Invalid donation date stored in the system."
            );
        }
    }


    // =========================================================
    // BLOOD AVAILABILITY
    // =========================================================

    public static void checkBloodAvailability() {

        String bloodGroup;

        while (true) {

            System.out.print("Enter Blood Group: ");

            bloodGroup =
                    sc.nextLine().toUpperCase();

            if (bloodGroup.equals("A+") ||
                    bloodGroup.equals("A-") ||
                    bloodGroup.equals("B+") ||
                    bloodGroup.equals("B-") ||
                    bloodGroup.equals("AB+") ||
                    bloodGroup.equals("AB-") ||
                    bloodGroup.equals("O+") ||
                    bloodGroup.equals("O-")) {

                break;
            }

            System.out.println(
                    "Invalid blood group."
            );
        }


        int units;

        while (true) {

            System.out.print(
                    "Enter Required Units: "
            );

            try {

                units = sc.nextInt();
                sc.nextLine();

                if (units >= 1 && units <= 10) {
                    break;
                }

                System.out.println(
                        "Units must be between 1 and 10."
                );

            } catch (Exception e) {

                System.out.println(
                        "Enter a valid number."
                );

                sc.nextLine();
            }
        }


        boolean available =
                inventoryManager.checkAvailability(
                        bloodGroup,
                        units
                );


        if (available) {

            System.out.println(
                    "Blood is available."
            );

        } else {

            System.out.println(
                    "Required blood is not available."
            );
        }
    }


    // =========================================================
    // ADMIN LOGIN
    // =========================================================

    public static void adminLogin() {

        System.out.println("\n==============================================");
        System.out.println("                ADMIN LOGIN");
        System.out.println("==============================================");

        System.out.print("Enter Admin Username: ");
        String username = sc.nextLine();

        System.out.print("Enter Admin Password: ");
        String password = sc.nextLine();


        // Admin credentials
        // Username : admin
        // Password : admin123

        if (username.equals("admin") &&
                password.equals("admin123")) {

            System.out.println(
                    "\nAdmin Login Successful."
            );

            System.out.println(
                    "Welcome Administrator."
            );


            AdminMenu adminMenu =
                    new AdminMenu();

            adminMenu.showAdminMenu();

        } else {

            System.out.println(
                    "Invalid Admin Username or Password."
            );
        }
    }
}
