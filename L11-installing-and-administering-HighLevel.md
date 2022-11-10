# Lesson 11 Lab Instructions

## Exercise 1: Automating Package Execution

The goal of this exercise is to review the process of using jobs to automate package executions. In this exercise,
 you will create a job to run the **DynamicPackage.dtsx** and schedule that job to run on
 two different
 schedules.

1. Change the NTFS permissions on the Chapter 10QA and Chapter 10Dev folders so that the Users (or Domain Users)
 group has Full Control of each folder.
2. Create a new job named **WeeklyPackage**.
3. Configure the first step of the WeeklyPackage job to execute the **DynamicPackage.dtsx** package
 deployed in Chapter 9.
4. Configure the package to use the QA environment and to use verbose logging.
5. Configure the package to include the job step details in the job history.
6. Schedule the package to run at 6pm on weekdays and at noon on weekends.
7. Test the job by running it manually.
8. Review the job history.
9. Review the report history.
10. If time permits, change the Configuration > Advanced Logging level property of the first job step to
 Performance, run the job again, and then view the differences of the detail level on the Messages report.