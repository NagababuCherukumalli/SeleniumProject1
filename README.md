 package base;
import java.io.File;
import java.text.SimpleDateFormat;
import java.util.*;
import java.io.IOException;
import java.util.concurrent.TimeUnit;

import config.*;

import org.apache.commons.io.FileUtils;

import org.openqa.selenium.Alert;
import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.Keys;
import org.openqa.selenium.NoSuchElementException;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.Point;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.Select;

import datatable.Xls_Reader;
import static org.testng.Assert.*;
public class BaseTest extends OR 
{
		
	public static Xls_Reader datatable_suite1=null;
	protected static BaseTest page;
	//public static BaseTest page;
	public BaseTest(WebDriver driver)
	{
		super(driver);
	}
	
	public static void initialize() throws Exception
	{
		datatable_suite1=new Xls_Reader(System.getProperty("user.dir")+"//src//config//TestData.xlsx");
		//datatable_suite1=new Xls_Reader("F:\\Selenium_\\DataDrivenframework\\src\\config\\TestData.xlsx");
	}
	//Login
	public void fillLogin(String uname, String upwd)
	{
		username.clear();
		username.sendKeys(uname);
		password.clear();
		password.sendKeys(upwd);
		login.click();
		
	}
	/*public void phonenumber(CharSequence[] st1)
	{
		 searchgroup.sendKeys(st1);
	}*/
	//OK
	public void clickOK()
	{
		Alert al=driver.switchTo().alert();
		al.accept();
	}
	//Cancel
	public void clickCancel()
	{
		Alert al=driver.switchTo().alert();
		al.dismiss();
	}
	
	//FundTrasfer
	/*public void fillPaydetails(String payeename,String amt,String remarks,String transpwd)
	{
		Select dd=new Select(dd_payeeName);
		dd.selectByValue(payeename);
		//dd.selectByIndex(payeename);
		tfield_amt.sendKeys(amt);
		tfield_remarks.sendKeys(remarks);
		tfield_transpassword.sendKeys(transpwd);
		btn_submit.click();
	}*/
	
	
	public void openURL(String url)
	{
		driver.manage().deleteAllCookies();
		driver.manage().window().maximize();
		driver.manage().timeouts().implicitlyWait(60,TimeUnit.SECONDS);  
		driver.get(url);
	}
			

		public String getTitle()
		{
		return driver.getTitle();
		}

		
public void scrollDown() throws InterruptedException
{
	JavascriptExecutor jse = (JavascriptExecutor)driver;
    jse.executeScript("window.scrollBy(0,250)", "");
    
   
           
    
    /*Actions actions = new Actions(driver);
    actions.keyDown(Keys.CONTROL).sendKeys(Keys.END).perform();*/
    
    
    }


public void DragAndDrop(WebElement st) throws InterruptedException
{
	 new Actions(driver)
     .dragAndDropBy(st,0,350)
     .build()
     .perform();
     Thread.sleep(5000);
}
		

		
	
	public void stopDriver()
	{
		
		driver.quit();
	}
	
		
	public static void takeScreenShots(String fileName) throws IOException{
		
		 File scrFile = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
	        FileUtils.copyFile(scrFile, new File(System.getProperty("user.dir")+"\\screenshots\\"+fileName+".png"));
	}
	

	public String randUserGen() 
	{
		Date d = new Date();
		SimpleDateFormat ft = new SimpleDateFormat("yyMMddhhmm");
		String strUser = ft.format(d);
		return strUser;
	}
		
	
	public void verifyElementPresent(WebElement e)
	{
		assertTrue(e.isDisplayed());
	}

	public void DragAndDrop1(WebElement drag) throws Exception {
		// TODO Auto-generated method stub
		 new Actions(driver)
	     .dragAndDropBy(drag,0,500)
	     .build()
	     .perform();
	     Thread.sleep(5000);
		
	}
	
	public void LinkS(String t) throws InterruptedException
	{
		elementHighlight(driver.findElement(By.linkText(t)));
		  driver.findElement(By.linkText(t)).click();
		  
			if(driver.getTitle().equals("Error 404"))
			{
				System.out.println("Link :"+t+ ": is not working");
			}
			else
			{
				
				System.out.println("Link :"+t+ ": is working fine");
				Thread.sleep(5000);
				driver.navigate().back();
				Thread.sleep(8000);
				driver.findElement(By.cssSelector("i.fa.fa-bars")).click();
				Thread.sleep(5000);
				
					System.out.println("**************************");
				
			}
	}
	
	
	
	public void AllValues(WebElement element)
	{
		verifyElementPresent(element);
		if(element.isEnabled())
		{
		System.out.println(element.getText()+"--------------->This Element Is Present");
		System.out.println("The Color Of The Element--------->:"+element.getCssValue("color"));
		
		 System.out.println("Font Size of The Element--------->:"+ element.getCssValue("font-size"));
		 System.out.println("To Get The Test Of The Element---->:"+element.getText());
		 
		 elementHighlight(element);
		 System.out.println("***************************************");	
		}
		else
		{
			System.out.println("Element is not Enabled");
		}
	}
	
	
	
	public String getFontWeight(WebElement element) {
		//Output will return as 400 for font-weight : normal, and 700 for font-weight : bold
		
		return element.getCssValue("font-weight");
		
		 
	}
	


public void elementHighlight(WebElement element) {
		for (int i = 0; i < 2; i++) {
			JavascriptExecutor js = (JavascriptExecutor) driver;
			js.executeScript(
					"arguments[0].setAttribute('style', arguments[1]);",
					element, "color: red; border: 3px solid red;");
			js.executeScript(
					"arguments[0].setAttribute('style', arguments[1]);",
					element, "");
		}
	}

public void select(WebElement e,int i) throws Exception
{
	 Select st=new Select(e);
	 st.selectByIndex(i);
	 WebElement op= st.getFirstSelectedOption();
	 System.out.println("The Drop Down Value is :"+op.getText());
	
	Thread.sleep(5000);
}




}
	

