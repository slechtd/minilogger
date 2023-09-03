## MiniLogger

MiniLogger is a minimalistic logging and reporting utility designed to be used with Selenium, Java, and TestNG based automation frameworks. It generates a JSON-based report at the end of the test run. This report can then be consumed by application that store or visualize the data.

### Requirements:
- Gson library for JSON serialization

## Usage

### Configuration

Firstly, you need to set the report file name and the path where the report should be saved:

<pre>
MiniLogger.setReportFileName("TestReport.json");
MiniLogger.setReportFilePath("/path/to/save/report");
</pre>

### Adding info

Information about the test execution can be added in key-value pair like so:

<pre>
MiniLogger.setInfo("Environment", "DEV");
</pre>

### Logging Information

To log information during test execution:

<pre>
//Basic log:
MiniLogger.log("Your log message", "TestCaseName");

//Pass a test:
MiniLogger.pass("Successfully logged in", "TestCaseName1");

//Fail a test:
MiniLogger.fail("Login Failed", "TestCaseName2");

//fail() also takes a throwable:
Throwable throwable = new Throwable("Some Exception");
MiniLogger.fail(throwable, "TestCaseName3");
</pre>

### Adding Screenshots

Here's a suggested usage with testNG Listeners. In this example, a test is failed and a screenshot path is attached to the report. Use your own implementation of captureScreenshot().

<pre>
@Override
public void onTestFailure(ITestResult result) {
  Throwable throwable = result.getThrowable();
  String testName = result.getName();
  MiniLogger.fail(throwable, testName);
  
  // If you also want to capture a screenshot on failure
  String screenshotPath = captureScreenshot(testName);
  MiniLogger.addScreenshot(screenshotPath, testName);
}
</pre>

### Generating The Report

Use flushReport() to generate the file in the specified directory. Using TestNG to make the call listeners is recommended.

<pre>
MiniLogger.flushReport();
</pre>
