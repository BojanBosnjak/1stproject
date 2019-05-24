# 1stproject
This is my 1st project for automation testing. I made script that is checking job apply functionality on Daon company web page.

namespace Testiranje
{
    public class TestKlasa
    {
        public void DaonJobApplication()
        {
            using (IWebDriver driver = new ChromeDriver())
            {
                driver.Manage().Timeouts().ImplicitWait = TimeSpan.FromSeconds(10); //određujem mu da mi na kraju da vremena da proverim unesene podatke
                driver.Url = "https://startit.rs/";
                //IWebElement myDynamicElement = driver.FindElement(By.CssSelector("#header-nav > li:nth-child(2) > a"));
                                
                driver.FindElement(By.CssSelector("#header-nav > li:nth-child(2) > a")).Click(); //Uz pomoć css selektora sam prolazio kroz startit.rs
                
                driver.FindElement(By.CssSelector("#poslovi-izdvojene-ikonice > a:nth-child(8) > div > img")).Click();

                driver.FindElement(By.CssSelector("#poslovi-listing > div > div:nth-child(1) > div > h1 > a")).Click();

                driver.SwitchTo().Window(driver.WindowHandles.Last());

                driver.FindElement(By.Id("so-co-dugme")).Click();

                driver.SwitchTo().Window(driver.WindowHandles.Last());
                
                driver.FindElement(By.XPath("//button[contains(text(), 'Apply')]")).Click(); //Prebacujem se na daoninc.bamboohr.com

                //sledi ddruga varijanta koda iznad

                /*driver.FindElement(By.CssSelector("body > div.container > div.ResAts__card.col-md-8.baseColorBg-before.js-jobs-left >" +
                    " div.ResAts__Viewport.js-jobs-viewport.js-chosen-container > div > div.ResAts__page.ResAts__description.js-jobs-page.js-jobs-description >" +
                    " div.ResAts__card-content.ResAts__card-content--footer.clearfix > div > button")).Click();*/
                //driver.Manage().Timeouts().ImplicitWait = TimeSpan.FromSeconds(10);  

                driver.FindElement(By.Id("firstName")).SendKeys("Bojan"); //Popunjavam podatke
                driver.FindElement(By.Id("lastName")).SendKeys("Bošnjak");
                driver.FindElement(By.Id("email")).SendKeys("bojanbos@gmail.com");
                driver.FindElement(By.Id("phone")).SendKeys("+381645047279");
                driver.FindElement(By.Id("address")).SendKeys("Preševska 53");
                driver.FindElement(By.Id("city")).SendKeys("Belgrade");
                driver.FindElement(By.CssSelector("#applicationForm > " +
                    "fieldset:nth-child(5) > div:nth-child(5) > div:nth-child(2) > div > input")).SendKeys("Central Serbia");
                driver.FindElement(By.Id("zip")).SendKeys("11000");


                driver.FindElement(By.CssSelector("#resumeUpload > span.attach-wrapper > a")).Click();

                /*Instalirao sam AutoIt biblioteku kao drugu opciju za upload biografije na sajt. 
                 Prethodni pokušaji da uploadujem biografiju nisu bili uspešni*/
                AutoItX3 autoIt = new AutoItX3();
                autoIt.WinActivate("File upload");
                autoIt.Send(@"C:\Users\Bojan Bosnjak\Desktop\Bojan Bošnjak C.V.pdf");
                Thread.Sleep(3000); //Ovde sam namerno koristio thread jer ne savetuju da se koriste implicitno i eksplicitno čekanje zajedno.
                autoIt.Send("{ENTER}");

                driver.FindElement(By.Id("dateAvailable")).SendKeys("01 Jun 2019");
                driver.FindElement(By.Id("salary")).SendKeys("number€");
                driver.FindElement(By.Id("linkedin")).SendKeys("https://www.linkedin.com/in/bojan-bo%C5%A1njak-61054614b/");

                //Elementi zakomentarisani ispod nisu uvek vidljivi. I kao takve sam morao da ih stavim u try - catch jer
                //kada ih sajt ne prikaže puca kod. U jednom od 10 slučajeva učitava dodatna pitanja.
                //Uspeo sam jednom prilikom da uhvatim elemente i da pokupim njihove css selektore i id kako bih napravio izuzetak.
                
                /*var elementList = new List<string> { "#higherEd_chzn > a", "customQuestion[80]", "customQuestion[81]",
                "customQuestion[94]", "customQuestion[104]"};

                try
                {
                    var element = driver.FindElement(By.CssSelector("#higherEd_chzn > a"));
                    if (element.Displayed)
                    {
                        driver.FindElement(By.CssSelector("#higherEd_chzn > a")).SendKeys("Some College");

                        driver.FindElement(By.Id("customQuestion[80]")).SendKeys("Yes");
                        driver.FindElement(By.Id("customQuestion[81]")).SendKeys("I will be available to start 1st of June 2019.");
                        driver.FindElement(By.Id("customQuestion[94]")).SendKeys("I found your job post on https://startit.rs/ web page");
                        driver.FindElement(By.Id("customQuestion[104]")).SendKeys("This application is sent using Selenium tool. " +
                            "As absolute beginner did some tests on your web page, and I will send you results in email. " +
                            "This might be considered as my motivational letter.");
                    }
                }
                catch (NoSuchElementException)
                {
                        RedMsg("Element nije prijakazan na stranici");
                }*/

                driver.FindElement(By.XPath("//button[contains(text()," +
                    " 'btn btnLarge btnAction js-jobs-submit-application addProcessing')]")).Click(); //Opcija 1 za klik na submit dugme

                /*driver.FindElement(By.CssSelector("body > div.container > " +   //opcija 2
                "div.ResAts__card.col-md-8.baseColorBg-before.js-jobs-left > " +
                "div.ResAts__Viewport.js-jobs-viewport.js-chosen-container > div >" +
                " div.ResAts__page.ResAts__application.ResAts__page--footer.js-jobs-page.js-jobs-application >" +
               " div.ResAts__card-content.ResAts__card-content--footer.clearfix > div > button")).Click();*/

                driver.Quit();

               
            }
        }

        public void GreenMsg(string msg)
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine(msg);
            Console.ForegroundColor = ConsoleColor.White;
        }
        public void RedMsg(string msg)
        {
            Console.ForegroundColor = ConsoleColor.Red;
            Console.WriteLine(msg);
            Console.ForegroundColor = ConsoleColor.White;
        }


    }
}
