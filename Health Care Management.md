# HCL-PT1
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Patient {
    private String id;
    private String name;
    private int age;
    private String gender;
    private String medicalHistory;

    public Patient(String id, String name, int age, String gender, String medicalHistory) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.gender = gender;
        this.medicalHistory = medicalHistory;
    }

    public String getId() {
        return id;
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

    public String getMedicalHistory() {
        return medicalHistory;
    }

    @Override
    public String toString() {
        return "ID: " + id + "\nName: " + name + "\nAge: " + age + "\nGender: " + gender + "\nMedical History: " + medicalHistory;
    }
}

class HealthcareManagementSystem {
    private List<Patient> patients;

    public HealthcareManagementSystem() {
        patients = new ArrayList<>();
    }

    public void registerPatient(Patient patient) {
        patients.add(patient);
        System.out.println("Patient registered successfully.");
    }

    public Patient findPatientById(String id) {
        for (Patient patient : patients) {
            if (patient.getId().equals(id)) {
                return patient;
            }
        }
        return null; // Patient not found
    }

    public void displayAllPatients() {
        System.out.println("\n--- List of Patients ---");
        for (Patient patient : patients) {
            System.out.println(patient);
            System.out.println("----------------------------");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        HealthcareManagementSystem healthcareSystem = new HealthcareManagementSystem();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nHealthcare Management System");
            System.out.println("1. Register Patient");
            System.out.println("2. Find Patient by ID");
            System.out.println("3. Display All Patients");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter patient ID: ");
                    String id = scanner.nextLine();
                    System.out.print("Enter patient name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter patient age: ");
                    int age = scanner.nextInt();
                    scanner.nextLine(); // Consume newline
                    System.out.print("Enter patient gender: ");
                    String gender = scanner.nextLine();
                    System.out.print("Enter patient medical history: ");
                    String medicalHistory = scanner.nextLine();

                    Patient newPatient = new Patient(id, name, age, gender, medicalHistory);
                    healthcareSystem.registerPatient(newPatient);
                    break;

                case 2:
                    System.out.print("Enter patient ID to search: ");
                    String searchId = scanner.nextLine();
                    Patient foundPatient = healthcareSystem.findPatientById(searchId);
                    if (foundPatient != null) {
                        System.out.println("\n--- Found Patient ---");
                        System.out.println(foundPatient);
                    } else {
                        System.out.println("Patient not found.");
                    }
                    break;

                case 3:
                    healthcareSystem.displayAllPatients();
                    break;

                case 4:
                    System.out.println("Exiting...");
                    scanner.close();
                    System.exit(0);
                    break;

                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
