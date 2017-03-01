# createticketfreshdesk3customfield

<?php 
# aditya
# $api_key = "API_KEY";

# $api_key = "xbsl5Gj2lTlwkFpNNdRd";

# adityafd2
$api_key = "SNkvr4kwbsI5F1mDEFLJ";
# adityafd2

# xbsl5Gj2lTlwkFpNNdRd

# adityafd2 (freshdesk2nd time)
# SNkvr4kwbsI5F1mDEFLJ
# adityafd2

# $password = "x";

$password = "navigant123";

# $yourdomain = "YOUR_DOMAIN";

# $yourdomain = "navigantech";

$yourdomain = "ntpl";

# https://navigantech.freshdesk.com/helpdesk/dashboard?view=standard

# adityafd2
# https://ntpl.freshdesk.com/api/v2/tickets
# adityafd2
# aditya




#echo $_GET['phonenumber'];

$ticket_data = json_encode(array(
  "description" => "Some details on the issue ...",
  "subject" => "Support needed..for aditya",
  "email" => "tawkirsid@ali.com",
  "priority" => 1,
  "status" => 2,
  "phone" => "9717589111",
 #  "phone" =>  $_GET['phonenumber'],
  # "custom_fields" => array( "propertytax_subject" => "adfromphp"),
    "custom_fields" => array( "propertytax_subject" => "adfromphp", "propertytax_filehead"=>"adityafilehedphp"),

  "cc_emails" => array("ram@freshdesk.com", "diana@freshdesk.com")
));


print_r($ticket_data);

# alert(book.title);
# alert(ticket_data.email);

$url = "https://$yourdomain.freshdesk.com/api/v2/tickets";
$ch = curl_init($url);
$header[] = "Content-type: application/json";
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_HEADER, true);
curl_setopt($ch, CURLOPT_USERPWD, "$api_key:$password");
curl_setopt($ch, CURLOPT_POSTFIELDS, $ticket_data);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$server_output = curl_exec($ch);
$info = curl_getinfo($ch);
$header_size = curl_getinfo($ch, CURLINFO_HEADER_SIZE);
$headers = substr($server_output, 0, $header_size);
$response = substr($server_output, $header_size);
if($info['http_code'] == 201) {
  echo "Ticket created successfully, the response is given below \n";
  echo "Response Headers are \n";
  echo $headers."\n";
  echo "Response Body \n";
  echo "$response \n";
} else {
  if($info['http_code'] == 404) {
    echo "Error, Please check the end point \n";
  } else {
    echo "Error, HTTP Status Code : " . $info['http_code'] . "\n";
    echo "Headers are ".$headers;
    echo "Response are ".$response;
  }
}
curl_close($ch);
?>

