# Wrapping 
package com.files;

import java.awt.AWTException;
import java.awt.Robot;
import java.awt.Toolkit;
import java.awt.datatransfer.StringSelection;
import java.awt.event.KeyEvent;
import java.util.ArrayList;
import java.util.Collection;
import java.util.Collections;
import java.util.List;
import java.util.NoSuchElementException;

import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class TG{
	
	WebDriver driver;
	
	public void upload() throws AWTException, InterruptedException {
		System.setProperty("webdriver.chrome.driver", ".\\Driver\\chromedriver.exe");
		driver=new ChromeDriver();
		driver.manage().window().maximize();
		driver.navigate().to("https://www.freepdfconvert.com/");
		driver.findElement(By.xpath("//*[@class='btn-wrapper upload-btn']")).click();
		String s="C:\\VM - 16-10\\Customer Management.png";
		StringSelection s1=new StringSelection(s);
		Toolkit.getDefaultToolkit().getSystemClipboard().setContents(s1, null);
		Thread.sleep(3000);
		Robot r=new Robot();
		r.keyPress(KeyEvent.VK_CONTROL);
		r.keyPress(KeyEvent.VK_V);
		r.keyRelease(KeyEvent.VK_CONTROL);
		r.keyRelease(KeyEvent.VK_V);
		r.keyPress(KeyEvent.VK_ENTER);
		
	}
	
	public void dyntabl() throws InterruptedException {
		driver.navigate().to("https://atlassian.design/components/dynamic-table/examples");
		JavascriptExecutor js=(JavascriptExecutor)driver;
		Thread.sleep(3000);
		WebElement tbl=driver.findElement(By.xpath("//*[@id=\"main\"]/main/div[2]/div[1]/div/div[2]/div/div/div[2]/div[1]/div[1]/table"));
		js.executeScript("arguments[0].scrollIntoView(true)", tbl);
		System.out.println(tbl.getText());
		List<WebElement> listweb=driver.findElements(By.xpath("//*[@id=\"main\"]/main/div[2]/div[1]/div/div[2]/div/div/div[2]/div[1]/div[1]/table/thead/tr/th"));
		int th=listweb.size();
		System.out.println(th);
		/*List<WebElement> listweb1=driver.findElements(By.xpath("//*[@id=\"main\"]/main/div[2]/div[1]/div/div[2]/div/div/div[2]/div[1]/div[1]/table/tbody/tr"));
		int tr=listweb1.size();
		System.out.println(tr);
		for(WebElement web:listweb1) {
			System.out.println(web.getText());
			if(web.getText().contains("george")) {
				web.click();
			}else {
				System.out.println("couldn't fount");
			}
		}*/
		List<String> values=new ArrayList<String>();
		List<WebElement> name=driver.findElements(By.xpath("//*[@data-rbd-droppable-id='dynamic-table-droppable'][@data-rbd-droppable-context-id=0]//td[4]"));
		for (WebElement webElement : name) {
			String ele=webElement.getText();
			values.add(ele);
		}
		System.out.println(values);
		int v=values.size();
		List<Integer> num=new ArrayList<Integer>();
		for (int i=0;i<=v-1;i++) {
			num.add(Integer.parseInt(values.get(i)));
		}
		System.out.println(num);
		
		int s=Collections.min(num);
		System.out.println(s);
		System.out.println(driver.findElement(By.xpath("//*[@data-rbd-droppable-id='dynamic-table-droppable'][@data-rbd-droppable-context-id=0]//td[text()="+"\""+s+"\""+"]")));
		WebElement s1=driver.findElement(By.xpath("//*[@data-rbd-droppable-id='dynamic-table-droppable'][@data-rbd-droppable-context-id=0]//td[text()="+s+"]"));
		s1.findElement(By.xpath("//following::td[1]")).click();
		//driver.findElement(By.xpath("//*[@data-rbd-droppable-id='dynamic-table-droppable'][@data-rbd-droppable-context-id=0]//td[text()="+s+"]//following::td[1]")).click();
	}
	
	public void datepick() throws InterruptedException,NoSuchElementException {
		Thread.sleep(3000);

		driver.navigate().to("https://atlassian.design/components/datetime-picker/examples");
		Thread.sleep(3000);

		driver.findElement(By.id("react-select-2-input")).click();
		driver.findElement(By.xpath("//*[@class='css-75mv6m'][2]")).click();
		driver.findElement(By.xpath("//*[text()=15]")).click();
		Thread.sleep(3000);		
		//driver.findElement(By.xpath("//*[@id='react-select-2-input']")).sendKeys("08/04/1995");
	}
	
	
	
	public static void main(String[] args) throws AWTException, InterruptedException {
		TG obj=new TG();
		obj.upload();
		obj.dyntabl();
		obj.datepick();
	}
	
}
