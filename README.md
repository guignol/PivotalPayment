PivotalPayment
==============
PHP Library for Pivotal Payment
http://www.pivotalpayments.com/ca/fr/



Requirements
-----------
CURL (php_curl)
XMLRPC (php_xmlrpc)
Multibyte String PHP extension (php_mbstring)

Installation
-----------
  Place the content of the github repo into the desired directory in your projet ($DIR)

Live Usage
-----------
  	//$DIR see section installation below
  	require_once($DIR.DIRECTORY_SEPARATOR.'Pivotal.php');	
	
	$pivotal_config = new Pivotal_Config('test');
	
	$card = $pivotal_config->readVendorTestCard('visa');

	$paymentParams['ORDERID'] = $orderId;
	$paymentParams['AMOUNT'] = $amount;
	$paymentParams['CURRENCY'] = $currency;
	$paymentParams['CARDNUMBER'] = $cardNumber;
	$paymentParams['CARDHOLDERNAME'] = $cardHolderName;
	//month two digits (09 for september)
	$paymentParams['MONTH'] = $cardMonth;
	//year two digits (16 for 2016)
	$paymentParams['YEAR'] = $cardYear;
	//CVV 3 or 4 Digits depending on vendor
  	$paymentParams['CVV'] = $cardCVV;

  	$pivotal = new Pivotal('test',$params);

  	$response = $pivotal->sendPayment();
	

Test Usage
-----------
Test cards are included in the library:

  	//$DIR see section installation below
  	require_once($DIR.DIRECTORY_SEPARATOR.'Pivotal.php');	
	
	$pivotal_config = new Pivotal_Config('test');
	
	//get test card number for the selected vendor (Visa)
	//get the holdername and CVV too
	//all test variables are under the Data Directory (TestCards.json)
	//live and Test URL are in Data Directory (MainConfig.json)
	//live and Test terminals are in Data Directory (Terminals.json)

	$card = $pivotal_config->readVendorTestCard('visa');
	
	$paymentParams['ORDERID'] = rand(10,10000);
	$paymentParams['AMOUNT'] = 1000;
	$paymentParams['CURRENCY'] = 'CAD';
	$paymentParams['CARDNUMBER'] = $card['CardNumber'];
	$paymentParams['CARDHOLDERNAME'] = $card['CardHolderName'];
	$paymentParams['MONTH'] = '09';
	$paymentParams['YEAR'] = '16';
  	$paymentParams['CVV'] = $card['CVV'];

  	$pivotal = new Pivotal('test',$params);

  	$response = $pivotal->sendPayment();
	

Extra
-----------
This Lib also provide Regex to detect card vendor (REGEX are located in Data/CardTypes.json)
and you can read the vendor based on the Card Number

 
	//$DIR see section installation below
  	require_once($DIR.DIRECTORY_SEPARATOR.'Pivotal.php');	
	
	$pivotal_config = new Pivotal_Config('test');

	//this clean and compare the card number to regular expression config located under Data/CardTypes.json
	//please feel free to add new credit card type but keep in mind the the order in the CardTypes.json is important and that last pattern found = output
	//so be sure to have VISA, MASTERCARD before resellers (VISA DEBIT is part of VISA for instance which means that VISA should be before VISA DEBIT)

	vendor = $pivotal_config->getCardType('1234567890123456');
	