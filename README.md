# PHPMailer SMTP Repository

This repository contains a simple example of using PHPMailer library to send emails via SMTP. PHPMailer is a popular library for sending email messages from PHP scripts.

## Prerequisites

- PHP installed on your system (version 5.5.0 or later recommended)
- Composer installed to manage dependencies

## Installation

1. Clone this repository to your local machine:

    ```
    git clone https://github.com/your-username/phpmailer-smtp.git
    ```

2. Navigate into the cloned directory:

    ```
    cd phpmailer-smtp
    ```

3. Install dependencies using Composer:

    ```
    composer install
    ```

## Configuration

1. Ensure that you have PHPMailer library included in your project. If not, you can include it by running:

    ```
    composer require phpmailer/phpmailer
    ```

2. Create a new PHP file and include the PHPMailerAutoload.php file:

    ```php
    <?php
    include('smtp/PHPMailerAutoload.php');
    ```
   
3. Customize the SMTP settings and email content:

    ```php
    echo smtp_mailer('to_email','Subject','html');
    
    function smtp_mailer($to, $subject, $msg) {
        $mail = new PHPMailer(); 
        $mail->IsSMTP(); 
        $mail->SMTPAuth = true; 
        $mail->SMTPSecure = 'tls'; 
        $mail->Host = "smtp.gmail.com";
        $mail->Port = 587; 
        $mail->IsHTML(true);
        $mail->CharSet = 'UTF-8';
        //$mail->SMTPDebug = 2; 
        $mail->Username = "email";
        $mail->Password = "password";
        $mail->SetFrom("email");
        $mail->Subject = $subject;
        $mail->Body = $msg;
        $mail->AddAddress($to);
        $mail->SMTPOptions = array('ssl'=>array(
            'verify_peer'=>false,
            'verify_peer_name'=>false,
            'allow_self_signed'=>false
        ));
        if(!$mail->Send()) {
            echo $mail->ErrorInfo;
        } else {
            return 'Sent';
        }
    }
    ?>
    ```

4. Replace `"email"` and `"password"` with your Gmail SMTP credentials and customize the email sending logic as needed.

5. Run the PHP script from the command line or through a web server.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
