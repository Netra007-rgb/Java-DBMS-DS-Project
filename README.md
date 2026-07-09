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
