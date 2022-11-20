# selenium-java

## Table of Contents

- [Xpath](#xpath)
- [CSS Selector](#css-selector)
- [Test Automation](#test-automation)

## Xpath
```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Xpath & CSS Selector</title>
</head>
<body>
    <div role="group" aria-label="card-wrapper">
      <div class="card" style="width: 18rem;">
          <div class="card-body">
              <h5 class="card-title">Card title</h5>
              <h6 class="card-subtitle mb-2 text-muted">Card subtitle</h6>
              <p class="card-text">Some quick example text to build on the card title</p>
              <a href="#" class="card-link" aria-label="card-link">Card link</a>
              <a href="#" id="another-76980" class="card-link" aria-label="another-link">Another link</a>
          </div>
      </div>
    </div>
</body>
</html>
```
**Relative:** Create Xpath from anywhere on a web page or we can directly grab the desire element if we've unique attribute using double forward slash (//). It's more safe since in here we don't need to maintain relationship from very first node 'html' to desire element.
```python
# Xpath Formula => //* or tagName[@attribute='attributeValue']
//a[@aria-label = 'card-link']
//div[@class='card-body']//h5
//div[@class='card-body']//h5[@class='card-title']
//div[@role='group']//h5
```
**Absolute:** It maintains relationships from very first 'html' tag to desire web element using single forward slash(/). If developer modify or remove any web element of absolute xpath in future, it will not work. 
```
/html/body/div/div/div/h5
```
**AND/OR:**
```
//a[@aria-label = 'card-link' and @class='card-link']
//a[@aria-label = 'card-link' or @class='card-link']
``` 
**text():** only used for text and it should be matched properly whatever mentioned on DOM. 
```
//p[text() = 'Some quick example text to build on the card title']
```
**contains():** used for text & html attribute both and match fully or partially with text or attribute value. No need to match exactly whatever mentioned on DOM, partial match should be okay
```
//p[contains(text(), 'on the card title')]
//p[contains(@class, 'card-text')]
```
**starts-with():** used to match from the starting characters of a text or attribute value 
```
//p[starts-with(text(), 'Some quick example')]
//a[starts-with(@id, 'another')]
```
**Ancestor/পূর্বপুরুষ:** It refers all previous elements if they have child-parent relationships
```html
//p[@class='card-text']//ancestor::html <!-- 1 of 1 -->
//p[@class='card-text']//ancestor::head <!-- 0 of 0 -->
```
**Descendant/বংশধর:** It refers all next elements if they have child-parent relationships
```html
//div[@role = 'group']//descendant::a <!-- 1 of 2 -->
//div[@role = 'group']//descendant::a[contains(@id, 'another')] <!-- 1 of 1 -->
```
**Preceding/পূর্ববর্তী:** It refers all previous elements if the don't have child-parent relationships.
```html
//p[@class='card-text']//preceding::html <!-- 0 of 0 -->
//p[@class='card-text']//preceding::head <!-- 1 of 1 -->
```
**Following Sibling:** It refers only the same level html elements. not upper or lower level.
```html
//h5[@class = 'card-title']//following-sibling::h6 <!-- 1 of 1 -->
//h5[@class = 'card-title']//following-sibling::a <!-- 1 of 2 -->
//h5[@class = 'card-title']//following-sibling::a[1] <!-- 1 of 1 -->
```
**Child:** represents all the child elements
```html
//div[@role= 'group']//child::a[1]
//div[@class= 'card-body']//child::a
//div[@class= 'card-body']//child::p
```
**Parent:** represents only the immediate parent element
```html
//a[contains(@id, 'another')]//parent::div <!-- refer immediate one (.card-) -->
```
**[⬆ back to top](#table-of-contents)**

## CSS Selector
```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Xpath & CSS Selector</title>
</head>
<body>
    <div role="group" aria-label="card-wrapper">
      <div class="card" style="width: 18rem;">
          <div class="card-body">
              <h5 class="card-title">Card title</h5>
              <h6 class="card-subtitle mb-2 text-muted">Card subtitle</h6>
              <p class="card-text">Some quick example text to build on the card title</p>
              <a href="#" class="card-link" aria-label="card-link">Card link</a>
              <a href="#" id="another-76980" class="card-link" aria-label="another-link">Another link</a>
          </div>
      </div>
    </div>
</body>
</html>
```
> CSS Selector Formula: tagName[attribute=value]
```html
a[aria-label = 'card-link']
a[aria-label='card-link'][class = 'card-link'] <!-- indicates multiple attr -->
```
**Child Element**
```html
div[role='group']>div>div>p <!-- '>' indicates immediate child only -->
div[role='group'] div p <!-- ' ' indicates immediate or not immediate child -->
```
**Class**
```html
<!-- '.' indicates class -->
.card-title
h5.card-title
a.card-link[aria-label='another-link']
h5[class='card-title']
a[id='another-76980'][class='card-link']
.card-subtitle.mb-2.text-muted <!-- indicates who has multiple classes -->
.card-link#another-76980 <!-- indicates who has class & id both -->
```
**ID**
```html
<!-- '#' indicates ID -->
#another-76980
a#another-76980
a#another-76980[aria-label='another-link']
a[id='another-76980']
a[id='another-76980'][class='card-link']
a#another-76980.card-link <!-- indicates who has class & id both -->
```
**[⬆ back to top](#table-of-contents)**

## Test Automation
**pom.xml**
```xml
<build>
	<plugins>
		<plugin>
			<groupId>org.apache.maven.plugins</groupId>
			<artifactId>maven-compiler-plugin</artifactId>
			<version>3.10.1</version>
			<configuration>
				<source>11</source>
				<target>11</target>
			</configuration>
		</plugin>
		<plugin>
			<groupId>org.apache.maven.plugins</groupId>
			<artifactId>maven-surefire-plugin</artifactId>
			<version>3.0.0-M7</version>
			<configuration>
				<suiteXmlFiles>
					<suiteXmlFile>testng.xml</suiteXmlFile>
				</suiteXmlFiles>
			</configuration>
		</plugin>
	</plugins>
</build>
<dependencies>
	<dependency>
		<groupId>org.seleniumhq.selenium</groupId>
		<artifactId>selenium-java</artifactId>
		<version>4.4.0</version>
	</dependency>
	<dependency>
		<groupId>io.github.bonigarcia</groupId>
		<artifactId>webdrivermanager</artifactId>
		<version>4.4.3</version>
	</dependency>
	<dependency>
		<groupId>org.testng</groupId>
		<artifactId>testng</artifactId>
		<version>6.14.3</version>
		<scope>compile</scope>
	</dependency>
	<dependency>
		<groupId>org.apache.logging.log4j</groupId>
		<artifactId>log4j-core</artifactId>
		<version>2.17.1</version>
	</dependency>
	<dependency>
		<groupId>org.apache.logging.log4j</groupId>
		<artifactId>log4j-api</artifactId>
		<version>2.17.1</version>
	</dependency>
	<dependency>
		<groupId>io.cucumber</groupId>
		<artifactId>cucumber-java</artifactId>
		<version>6.11.0</version>
	</dependency>
	<dependency>
		<groupId>io.cucumber</groupId>
		<artifactId>cucumber-testng</artifactId>
		<version>6.11.0</version>
	</dependency>
</dependencies>
```
**[⬆ back to top](#table-of-contents)**
#### src/main/java
**com.basepage.BasePage**
```java
public class BasePage {
	public static Logger log;
	public static Properties props;
	public static WebDriver driver;
	
	public BasePage() {
		log = LogManager.getLogger(BasePage.class);
		
		try {
			props = new Properties();
			String file_path = System.getProperty("user.dir") + "\\src\\main\\resources\\config.properties";
			FileInputStream fis = new FileInputStream(file_path);
			props.load(fis);
		} catch (FileNotFoundException e) {
			System.out.println(e.getMessage());
		} catch (IOException e) {
			System.out.println(e.getMessage());
		}
	}
	
	public void init() {
		if (props.getProperty("browser").equals("chrome")) {
			WebDriverManager.chromedriver().setup();
			driver = new ChromeDriver();
			log.info("***** ChromeDriver Initiated *****");
		} else if (props.getProperty("browser").equals("firefox")) {
			WebDriverManager.firefoxdriver().setup();
			driver = new FirefoxDriver();
			log.info("***** FirefoxDriver Initiated *****");
		} else {
			System.out.println("Driver not Found!");
		}
		driver.manage().deleteAllCookies();
		driver.manage().window().maximize();
		driver.manage().timeouts().pageLoadTimeout(Duration.ofSeconds(50));
		driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));
		driver.get(props.getProperty("URL"));
		log.info("***** Home page opened *****");
	}
}
```
**com.pagefactory.LoginPage**
```java
public class LoginPage {
	/*--- another way to initiate PageFactory ---
	public LoginPage(WebDriver driver) {
		PageFactory.initElements(driver, this);
	}
	---------------------------------------------*/
	@FindBy(xpath = "//input[@name = 'username']")
	private WebElement username;

	@FindBy(xpath = "//input[@name = 'password']")
	private WebElement password;
	
	@FindBy(xpath = "//button[@type = 'submit']")
	private WebElement loginBtn;
	
	@FindBy(css = ".oxd-text.oxd-text--p.oxd-alert-content-text")
	private WebElement errorMsg;
	
	@FindBy(css = ".oxd-text.oxd-text--h6.oxd-topbar-header-breadcrumb-module")
	private WebElement dashboardTxt;
	
	public WebElement getUsername() {
		return username;
	}

	public WebElement getPassword() {
		return password;
	}

	public WebElement getLoginBtn() {
		return loginBtn;
	}
	
	public WebElement getErrorMsg() {
		return errorMsg;
	}
	
	public WebElement getDashboardTxt() {
		return dashboardTxt;
	}
}
```
**[⬆ back to top](#table-of-contents)**

**features>login.feature**
```gherkin
#Author: Nazmul Hoque

@smoke
@core_regression
Feature: OrangeHRM Login Feature

	Background:
		Given go to the home page

  @smoke
  @core_regression
  @OrangeHRM_44001
  Scenario: User should able to login with valid username and password
    When input the username
    And input the password
    And click on login button
		Then validate the dashboard page
    
    
  @smoke
  @core_regression
  @OrangeHRM_44002
  Scenario: User should not able to login with valid username and invalid password
    When input the username and password
    | username | password |
    | Admin    | test123  |
    | Admin    | hello123 |
    And click on login button
		Then check invalid credentials

  @smoke
  @core_regression
  @OrangeHRM_44003
  Scenario Outline: User should not be able to login with invalid username and password
    When input the username <username>
    And input the password <password>
    And click on login button
		Then check invalid credentials

    Examples: 
      | username  | password |
      | test1     | test123  |
      | test2     | test456  |
      | test3     | test789  |
```
#### src/test/java
**com.stepdefs.LoginStepDef**
```java
public class LoginStepDef extends BasePage {
	LoginPage pf;
	
	@Given("go to the home page")
	public void go_to_the_home_page() {
        // pf = new LoginPage(driver); (another way to pass driver for PageFactory.initElements())
		pf = PageFactory.initElements(driver, LoginPage.class);
	}

	@When("input the username")
	public void input_the_username() {
		pf.getUsername().sendKeys(props.getProperty("username"));
	}

	@When("input the password")
	public void input_the_password() {
		pf.getPassword().sendKeys(props.getProperty("password"));
	}

	@When("click on login button")
	public void click_on_login_button() {
		pf.getLoginBtn().click();
	}

	@Then("validate the dashboard page")
	public void validate_the_dashboard_page() {
		Assert.assertEquals(pf.getDashboardTxt().getText(), "Dashboard");
		log.info("***** Login Successful *****");
	}
	
	@Then("check invalid credentials")
	public void check_invalid_credentials() {
		Assert.assertEquals(pf.getErrorMsg().getText(), "Invalid credentials");
		log.info("***** Login not Successful *****");
	}

	@When("input the username and password")
	public void input_the_username_and_password(DataTable dataTable) {
		List<Map<String, String>> data = dataTable.asMaps();
		
		pf.getUsername().sendKeys(data.get(0).get("username"));
		pf.getPassword().sendKeys(data.get(0).get("password"));
	}

	@When("input the username test1")
	public void input_the_username_test1() {
		pf.getUsername().sendKeys("test1");
	}

	@When("input the password test123")
	public void input_the_password_test123() {
		pf.getPassword().sendKeys("test123");
	}

	@When("input the username test2")
	public void input_the_username_test2() {
		pf.getUsername().sendKeys("test2");
	}

	@When("input the password test456")
	public void input_the_password_test456() {
		pf.getPassword().sendKeys("test456");
	}

	@When("input the username test3")
	public void input_the_username_test3() {
		pf.getUsername().sendKeys("test3");
	}

	@When("input the password test789")
	public void input_the_password_test789() {
		pf.getPassword().sendKeys("test789");
	}
}
```
**[⬆ back to top](#table-of-contents)**

**com.hooks.OrangeHrmHooks**
```java
public class OrangeHrmHooks extends BasePage {
	@Before
	public void setup() {
		init();
	}
	
	@After
	public void tearDown() {
		driver.quit();
		log.info("***** WebDriver Quit *****");
	}
}
```
**com.runner.CucumberRunner**
```java
@CucumberOptions(
	plugin= {"pretty","json:target/cucumber.json" }, // for html= {"com.cucumber.listener.ExtentCucumberFormatter:target/cucumber-reports/report.html" },	
	features = {".//features/"}, 
    glue = {"com.stepdefs","com.hooks"}, 	
    tags = "@OrangeHRM_44001 or @OrangeHRM_44002",
	dryRun = false, 
	monochrome = true
)

public class CucumberRunner extends AbstractTestNGCucumberTests {

}
```
**testng.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="OrangeHrmTestAutomation" verbose="1">
	<test name="OrangeHRM Login Test">
		<classes>
			<class name="com.runner.CucumberRunner" />
		</classes>
	</test>
</suite>
<!-- *************** Dummy Test Suite ***************
<suite name="Dummy Suite" parallel="tests" thread-count="5">
	<listeners>
		<listener class-name="com.listener.TestListener"></listener>
	</listeners>
	<test name="Dummy">
		<parameter name="url" value="dummy.website.com" />
		<groups>
			<run>
				<exclude name="smoke" />
				<include name="core_regression" />
			</run>
		</groups>
		<packages>
			<package name="com.dummy" />
		</packages>
		<classes>
			<class name="com.runner.CucumberRunner">
				<methods>
					<exclude name="dummy"></exclude>
					<include name="mobile.*"></include>
				</methods>
			</class>
		</classes>
	</test>
</suite>
************************************************** -->
```
**[⬆ back to top](#table-of-contents)**

#### src/main/resource
**config.properties**
```
browser = chrome
URL = https://opensource-demo.orangehrmlive.com/web/index.php/auth/login
username = Admin
password = admin123
```
**log4j2.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="WARN">
	<Properties>
		<Property name="basePath">./logs</Property>
	</Properties>

	<Appenders>
		<RollingFile name="File" fileName="${basePath}/app.log" filePattern="${basePath}/app-%d{yyyy-MM-dd}.log">
			<PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n" />
			<SizeBasedTriggeringPolicy size="500" />
		</RollingFile>
		<Console name="Console" target="SYSTEM_OUT">
			<PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n" />
		</Console>
	</Appenders>
	<Loggers>
		<Root level="trace">
			<AppenderRef ref="File" />
			<AppenderRef ref="Console" />
		</Root>
	</Loggers>
</Configuration>
```
**[⬆ back to top](#table-of-contents)**
