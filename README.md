import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the number of students");
        int number = sc.nextInt();
        sc.nextLine();
        List<String[]> list = new ArrayList<>();

        int sum = 0;
        for (int i = 0; i < number; i++) {
            System.out.println("Enter the name of the " + (i + 1) + "th student");
            String name = sc.nextLine();
            System.out.println("Enter the corresponding score");
            int grade = sc.nextInt();
            sc.nextLine();

            list.add(new String[]{name, String.valueOf(grade)});
            sum += grade;
        }

        double average = (double) sum / number;
        System.out.println("The grade point average is: " + average);

        System.out.println("Students and their grades:");
        for (String[] student : list) {
            System.out.println("Name: " + student[0] + ", Grade: " + student[1]);
        }

        while (true) {
            System.out.println("What function do you want to implement?");
            System.out.println("A: Add a new student");
            System.out.println("B: Find a student's score");
            System.out.println("C: Delete a student");
            System.out.println("D: Exit");
            String choice = sc.nextLine();
            switch (choice.toUpperCase()) {
                case "A":
                    System.out.println("Enter the name of the new student");
                    String newName = sc.nextLine();
                    System.out.println("Enter the grade of the new student");
                    int newGrade = sc.nextInt();
                    sc.nextLine(); // Consume the newline left in the buffer
                    list.add(new String[]{newName, String.valueOf(newGrade)});
                    break;
                case "B":
                    System.out.println("Enter the name of the student you want to find");
                    String theName = sc.nextLine();
                    for (String[] student : list) {
                        if (theName.equals(student[0])) {
                            System.out.println(theName + "'s score is " + student[1]);
                            break;
                        }
                    }
                    System.out.println("Student not found");
                    break;
                case "C":
                    System.out.println("Enter the name of the student you want to delete");
                    String nameToDelete = sc.nextLine();
                    boolean removed = list.removeIf(student -> nameToDelete.equals(student[0]));
                    if (removed) {
                        System.out.println("Student removed successfully");
                    } else {
                        System.out.println("Student not found");
                    }
                    break;
                case "D":
                    sc.close();
                    return;
                default:
                    System.out.println("Invalid choice. Please choose A, B, C, or D.");
            }
        }
    }
}
