---
type: rule
archivedreason: The rule has been replaced by https://rules.ssw.com.au/follow-naming-conventions-for-tests-and-test-projects
title: Do you follow the standard naming conventions for tests?
guid: 5a6283ea-18d8-4586-a696-06ef05660ce5
uri: do-you-follow-the-standard-naming-conventions-for-tests
created: 2020-03-11T20:18:31.0000000Z
authors:
- id: 1
  title: Adam Cogan
related: []

---

Hi Adam,

As well as keeping your code tidy, using this naming convention also allows you to use TestDriven.Net's 'Go To Test/Code' command.
This navigates between your tests and code under test (and back). This is something that test-driven developers end up doing a lot.
Screen captures at https://weblogs.asp.net/nunitaddin/testdriven-net-3-0-all-systems-go

- Jamie Cansdale

<!--endintro-->


| **Test Object**  | **Recommended Style**  | **Example**  |
| --- | --- | --- |
| Project Name | Tests.[Testtypes].Projectname | Tests.Unit.Common,Tests.Unit.WebFrontend,Test.Integration.MainWCFService<br>Tests.Functional.SilverlightUI, Tests.Functional.WebUI \* |
| Test Fixture Name | [Type]Tests | OrdersTests, CustomerTests, DeveloperTests |
| Test Case | [Function]Test | NullableIntTryParse\_NumberIsValid1\_Return1, StringHelperEncodeTo64\_EncodeAndUnencodeString\_ReturnSameString |
| Set Up | SetUp |   |
| Tear Down | TearDown |   |




\*Test types are categorized into "Unit" "Integration" or "Functional" tests, as explained in "[2. What are the different types of test you can have?](https://www.ssw.com.au/ssw/Standards/Rules/RulesToBetterUnitTests.aspx#TypesOfTests)"

The main reason why we are categorizing tests is so that we can run different test suites. Eg.

* Unit tests on Gated Checkin
* Integration tests after each check in on the build server
* All tests including the functional tests in the nightly build


**Samples for Naming of test projects** 
Test.Unit.WebUI: This test project, tests the WebUI project, and is independent of external resources.
That means all tests must pass.
Test.Integration.WebUI: This test project tests the WebUI and depends on other external resources (Eg. probably needs a database, web services, etc.).
That means if any external resource is unavailable, the tests will fail.
Tests.Functional.SilverlightUI: Tests the Silverlight UI from an end-user perspective by clicking around in the application
<dl class="goodImage">&lt;dt&gt;
      <img src="UnitTestsProject.jpg" alt="UnitTestsProject.jpg">
   &lt;/dt&gt;<dd>Figure: Good example - Naming for a Unit Test Project</dd></dl>Samples Naming of test methods
[TestMethod]
 public void Test\_Client()


::: bad
Bad example: There is no way to guess what this test does; you have to read the source

:::


[TestMethod]
 public void PubSubServiceConnectTest\_AuctionOk\_AuctionInfoReturned()


::: good
Good Example: We are testing PubSubService.Connect under the scenario that the "Auction status is OK" with an expected behaviour that data is returned
:::


Sample Code for Integration Tests:

using System;
using System.Collections;
using System.Data;
using System.Data.SqlClient;
using NUnit.Framework;
using SSW.NetToolKit.BusinessService;
using SSW.NetToolKit.DataAccess;
namespace SSW.NETToolkit.IntegrationTests
  {
  [TestFixture]
  Public class CustomerTests
    {
    BusinessRules business=new BusinessRules();     
    [Test]
    public void OrderTotal\_SimpleExampleInput()
        {
        decimal calculatedGrandTotal = business.CalculateOrderGrandTotal(10248);
        int expected = 440;
        Assert.AreEqual(expected, calculatedGrandTotal, "Calculated grand total didn't match the expect
        }
    [Test]
    public void OderTotal\_Discounts()
        {
        decimal calculatedGrandTotal = business.CalculateOrderGrandTotal(10260);
        decimal expected = 1504.65m;
        Assert.AreEqual(expected, calculatedGrandTotal, "Calculated grand total didn't match the expecte
        }
    [Test]
    public void RoundingTest\_RoundUp()
        {
        Assert.AreEqual(149.03, business.ApplyRounding(149.0282m), "Incorrect rounding rules applied for
        }
    [Test]
    public void RoundingTest\_RoundDown()
        {
        Assert.AreEqual(149.02, business.ApplyRounding(149.0232m), "Incorrect rounding rules applied     
        }
    [Test]
    public void RoundingTest\_NoRoundingNeeded()
        {
        Assert.AreEqual(149.02, business.ApplyRounding(149.02m), "Incorrect rounding rules applied for     
        }
    [Test]
    public void RoundingTest\_BorderCondition()
        {
        Assert.AreEqual(149.02, business.ApplyRounding(149.025m), "Incorrect rounding rules applied for
        }
    }
  }
<dl class="image">&lt;dt&gt;<img src="TestGenerationSettings.gif" alt="TestGenerationSettings.gif">&lt;/dt&gt;<dd>Figure: This rule is consistent with the Visual Studio default</dd></dl>**Tip:** You can create a test project using the Unit Test Wizard: Test > Add New Test

<dl class="image">&lt;dt&gt;<img src="AddNewTest.gif" alt="AddNewTest.gif">&lt;/dt&gt;<dd>Figure: Unit Test Wizard 1</dd></dl><dl class="image">&lt;dt&gt;<img src="CreateUnitTests.gif" alt="CreateUnitTests.gif">&lt;/dt&gt;<dd>Figure: Unit Test Wizard 2</dd></dl>