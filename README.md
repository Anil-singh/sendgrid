## Sendgrid - Send email and get email status using Sendgrid WEB API call.
Sendgrid module contains code in php to send email through sendgrid and get email stats from sendgrid using web api calls

## Example - Executing curl request
    function executeCurl ($request,$params){     
      // Generate curl request
      $session = curl_init($request);
      // Tell curl to use HTTP POST
      curl_setopt ($session, CURLOPT_POST, true);
      //curl_setopt($session, CURLOPT_SAFE_UPLOAD, true);
      // Tell curl that this is the body of the POST
      curl_setopt ($session, CURLOPT_POSTFIELDS, $params);
      // Tell curl not to return headers, but do return the response      
      curl_setopt($session, CURLOPT_HEADER, false);      
      curl_setopt($session, CURLOPT_ENCODING, 'gzip,deflate' );
      curl_setopt($session, CURLOPT_RETURNTRANSFER, true);
      // obtain response
      $response = curl_exec($session);
      //print_r(expression)
      curl_close($session);
      return $response;
    }
  ## Example - Send email
  
	$params = array(
	'api_user'  => $this->user,
	'api_key'   => $this->pass,
	'replyto'   => $replyTo,
	'subject'   => $subject,
	'html'      => $HTML_Body,
	'text'      => $TextBody,
	'from'      => $fromMail,
	'fromname'  => $fromName,
	);
      // Adding cc
      foreach($ccMail_arr as $cc) {
          $toMail_arr = array_merge($toMail_arr, $cc);
      }
      // Adding to
      for($i=0; $i<count($toMail_arr); $i++)
      {
        if($toMail_arr[$i]!="")
          $params['to['.$i.']'] = $toMail_arr[$i];
      }
       
      // Adding bcc
      for($b=0; $b<count($bccMail_arr); $b++)
      {
        if($bccMail_arr[$b]!="")
          $params['bcc['.$b.']'] = $bccMail_arr[$b];
      }      
      // Adding attachement list
      $Attach_File_Lists = $Attach_File_List; 
      foreach( $Attach_File_Lists as $Attach_File_List )
      {
        $fileName = $Attach_File_List['name'];        
        if(file_exists(MainUploadFolderPath.$fileName) && MainUploadFolderPath.$fileName!="")
        {
          $params['files['.$fileName.']'] = '@'.MainUploadFolderPath.$fileName;          
        }
      }
    
      $request  =  $this->url.'api/mail.send.json';
      $response = $this->executeCurl( $request, $params );

### Getting sendgrid stats
      $request =  $this->url.'api/stats.get.json';
      $params = array(
        'api_user'   => $this->user,
        'api_key'    => $this->pass,
        'start_date' => $start_date,
        'end_date'   => $end_date,
        'data_type'  => 'global',
        'metric'     => 'all'
      ); 
## Installation
### Replace configs variables - config.php
	/* from email */
	define('FROM_EMAIL', '');
	/* from name */
	define('FROM_NAME', '');
	/* reply email */
	define('REPLY_TO', ''); 
	/* sendgrid user name */
	define('SENDGRID_USER', '');
	/* sendgrid user password */
	define('SENDGRID_PASS', '');
	/* sendgrid user password */
	define('SENDGRID_API_URL', 'https://api.sendgrid.com/');
	/*MainUploadFolderPath*/
	define('MainUploadFolderPath','/uploads');
   
