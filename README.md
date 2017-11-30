# Microsoft Powerapps Bank App:

## This a bank app using power apps, a test of capabilities of Microsoft Powerapps.

# 1. Launch Screen:

## On this screen you enter the Login Screen through the photo. In this photo you have the "reset function" applied to different "text fields" so that no data is saved from any past session:
 
Reset([@passwordLoginScreenTextfield]); Reset([@usernameLoginScreenTextfield]); 
Reset([@findEmailForgotUsernameScreenTextfield]); 
Reset([@firstSecurityQuestionAnswerTextfield]); 
Reset([@secondSecurityQuestionAnswerTextfield]); 
Reset([@newPasswordInputTextfield]); 
Reset([@emailBasicInformationTextfield]); 
Reset([@usernameBasicInformationTextfield]); 
Reset([@passwordBasicInformationScreenTextfield]); 
Reset([@confirmPasswordBasicInformationScreenTextfield]); 
Reset([@firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield]); 
Reset([@mobileAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@firstNameAccountCreationTextfield]); 
Reset([@lastNameAccountCreationTextfield]); 
Reset([@firstSocialSecurityDigitsTextfield]); 
Reset([@secondSocialSecurityDigitsTextfield]); 
Reset([@thirdSocialSecurityTextfield]); 
Reset([@dateOfBirthDatepicker]); 
Reset([@firstSecurityQuestionDropdown]); 
Reset([@secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown]); 
Reset([@agreementCheckbox]); 
Navigate('Login Screen', ScreenTransition.Fade)

# 2. Login Screen:

## In this screen we can observe two "text fields", one of "Username" and "Password", three buttons, one of "Sign in", "Cancel" and "Create Account":
 
### a. The "Sign In", in the OnSelect property, validates the user and the "password", using a function called "LookUp", which looks for the record in the "Customer" table to validate it and give access to the "Main Screen" "using a function called" Navigate ", if the user is not validated, two labels appear using the UpdateContext function, which creates a global variable which is called with the value" false "in the OnVisible property in the" Screen ", this global variable is applied to the Visible property in the" labels "so that when an" If "condition executes UpdateContext with true, then the label appears, which is two" X "red and does not execute the function of navigation to go to the "Main Screen":

If(LookUp('[dbo].[Customer]', Username = usernameLoginScreenTextfield.Text, PasswordField = passwordLoginScreenTextfield.Text), Navigate([@'Main Screen'], ScreenTransition.Fade),!LookUp('[dbo].[Customer]', Username = usernameLoginScreenTextfield.Text,PasswordField = passwordLoginScreenTextfield.Text), UpdateContext({usernameVisible:true,passwordVisible:true}))
 
### b. The "Cancel" button, use the Navigate function to take you to the LaunchScreen and execute the Reset function in all text fields:

Reset([@passwordLoginScreenTextfield]); Reset([@usernameLoginScreenTextfield]); 
Reset([@findEmailForgotUsernameScreenTextfield]); 
Reset([@firstSecurityQuestionAnswerTextfield]); 
Reset([@secondSecurityQuestionAnswerTextfield]); 
Reset([@newPasswordInputTextfield]); 
Reset([@emailBasicInformationTextfield]); 
Reset([@usernameBasicInformationTextfield]); 
Reset([@passwordBasicInformationScreenTextfield]); 
Reset([@confirmPasswordBasicInformationScreenTextfield]); 
Reset([@firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield]); 
Reset([@mobileAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@firstNameAccountCreationTextfield]); 
Reset([@lastNameAccountCreationTextfield]); 
Reset([@firstSocialSecurityDigitsTextfield]); 
Reset([@secondSocialSecurityDigitsTextfield]); 
Reset([@thirdSocialSecurityTextfield]); 
Reset([@dateOfBirthDatepicker]); 
Reset([@firstSecurityQuestionDropdown]); 
Reset([@secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown]); 
Reset([@agreementCheckbox]);
Navigate([@'Launch Screen'],ScreenTransition.Fade)
 
### c. The "Account Creation" button performs the Navigate function and takes you to the "Account Creation Basic Information Screen" screen:

Navigate([@'Account Creation Basic Information Screen'], ScreenTransition.Fade)

# 3. Account Creation Basic Information Screen:

## We observe textfields, email, username, password, confirm password, "Next" button, "Load" button and "I already have an account" button to go back to the "Sign in Screen":
 
### a. Screen:

UpdateContext({passwordVisible:false})
 
### b. Button "Next":

If(!(passwordBasicInformationScreenTextfield.Text = confirmPasswordBasicInformationScreenTextfield.Text), UpdateContext({passwordVisible:true}));If(!IsBlank(passwordBasicInformationScreenTextfield.Text) And (passwordBasicInformationScreenTextfield.Text = confirmPasswordBasicInformationScreenTextfield.Text),Navigate([@'Account Creation Security Questions Screen'], ScreenTransition.Fade))
 
### c. Button "Load", saves temporarily in the application, in its cache, in collections, a function of ClearCollect that keeps a record every time the data is called, in this case it is stored saved due to lack of connection in one of the save screens the data, if there is a connection, call all that is called ImportedAccountCreation and with the Patch function, save the fields in the Customer table, if there is no connection, with the Navigate function, it takes you to the Account Creation Connection screen Timer, as the last attempt to save the locally recorded data:

ClearCollect(ImportedAccountCreation, loadAccountCreationData.Data); If(Connection.Connected,(ForAll(ImportedAccountCreation, Patch('[dbo].[Customer]', Defaults('[dbo].[Customer]'),{Username: Username, PasswordField: PasswordField, EmailAddress: EmailAddress, SecurityQuestion1: SecurityQuestion1, SecurityAnswer1:SecurityAnswer1, SecurityQuestion2: SecurityQuestion2, SecurityAnswer2: SecurityAnswer2, MobileNumber: MobileNumber, FirstName: FirstName, LastName: LastName, SocialSecurityNumber:SocialSecurityNumber, DateOfBirth: DateOfBirth, TermsAgreement: TermsAgreement}))),Connection.Connected,Navigate([@'Login Screen'],ScreenTransition.Fade),!Connection.Connected,Navigate([@'Account Creation Connection Timer Screen'],ScreenTransition.Fade))
 
### d. "I already have an account" button takes you to the "Login Screen" and executes the Reset function of all the Account Creation and Login Screen fields:

Navigate([@'Login Screen'], ScreenTransition.Fade);
Reset([@passwordLoginScreenTextfield]);
Reset([@usernameLoginScreenTextfield]); 
Reset([@findEmailForgotUsernameScreenTextfield]); 
Reset([@firstSecurityQuestionAnswerTextfield]); 
Reset([@secondSecurityQuestionAnswerTextfield]); 
Reset([@newPasswordInputTextfield]); 
Reset([@emailBasicInformationTextfield]); 
Reset([@usernameBasicInformationTextfield]); 
Reset([@passwordBasicInformationScreenTextfield]); 
Reset([@confirmPasswordBasicInformationScreenTextfield]); 
Reset([@firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield]);
Reset([@mobileAccountCreationSecurityQuestionsScreenTextfield]);
Reset([@firstNameAccountCreationTextfield]); 
Reset([@lastNameAccountCreationTextfield]); 
Reset([@firstSocialSecurityDigitsTextfield]); 
Reset([@secondSocialSecurityDigitsTextfield]); 
Reset([@thirdSocialSecurityTextfield]); 
Reset([@dateOfBirthDatepicker]); 
Reset([@firstSecurityQuestionDropdown]); 
Reset([@secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown]); 
Reset([@agreementCheckbox]); 
Navigate('Login Screen', ScreenTransition.Fade)

# 4. Account Creation Security Questions Screen:

## Two dropdown menus that load a clear collect by defallo in the OnVisible property of the Account Creation Security Questions Screen, two textfields to put conestaciones of the security questions, a textfield to put a phone number, a back button and a next button:
 
### a. Screen, OnVisible property:

ClearCollect(Security_Questions, {Question:"Choose"}, {Question:"What city were you born?"},{Question:"In what city was your first job?"},{Question:"What is the middle name of your youngest child?"}, {Question:"What was the make and model of your first car?"}, {Question:"What was your high school mascot?"}, {Question:"What is your oldest sibling's birthday month and year?"}, {Question:"What was the last name of your 3rd grade teacher?"}, {Question:"In what city does your nearest sibling live?"}, {Question:"What street did you live on in 6th grade?"}, {Question:"What was the name of your first pet?"}, {Question:"What is your favorite vacation spot?"}, {Question:"What was your childhood nickname?"}); UpdateContext({visible: false});UpdateContext({typeSecurityAnswer:false});UpdateContext({SameQuestion: false})
 
### b. Drop Down Menu 1, Items property:

Distinct(Security_Questions, Question)
 
### c. Drop Down Menu 2, Items property:

Distinct(Security_Questions, Question)
 
### d. Back button, OnSelect property:

Back(ScreenTransition.Fade)
 
### e. Next button, OnSelect property:

If(firstSecurityQuestionDropdown.Selected.Result Or secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown.Selected.Result = "Choose", UpdateContext({visible:true}),!IsBlank(firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield.Text) And !IsBlank(secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield.Text) And !(firstSecurityQuestionDropdown.Selected.Result = secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown.Selected.Result), Navigate([@'Account Creation Personal Details Screen'], ScreenTransition.Fade)); If(IsBlank(firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield.Text) Or IsBlank(secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield.Text), UpdateContext({typeSecurityAnswer:true}));If(firstSecurityQuestionDropdown.Selected.Result = secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown.Selected.Result, UpdateContext({SameQuestion:true}));If(!(firstSecurityQuestionDropdown.Selected.Result = secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown.Selected.Result), UpdateContext({SameQuestion:false}))

# 5. Account Creation Personal Details Screen

## First name, Last name, three conditionalized Social Security Number textfields, date pick control, text mark check, back button, cancel button and create account button:
 
### a. Screen OnVisible Property:

UpdateContext({AccountExists: false})
 
### b. Back Icon, OnSelect Property:

Back(Fade)
 
### c. Cancel Icon, OnSelect Property:

Navigate([@'Login Screen'],ScreenTransition.Fade);Reset([@passwordLoginScreenTextfield]); Reset([@usernameLoginScreenTextfield]); 
Reset([@findEmailForgotUsernameScreenTextfield]); 
Reset([@firstSecurityQuestionAnswerTextfield]); 
Reset([@secondSecurityQuestionAnswerTextfield]); 
Reset([@newPasswordInputTextfield]); 
Reset([@emailBasicInformationTextfield]); 
Reset([@usernameBasicInformationTextfield]); 
Reset([@passwordBasicInformationScreenTextfield]); 
Reset([@confirmPasswordBasicInformationScreenTextfield]); 
Reset([@firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield]); 
Reset([@mobileAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@firstNameAccountCreationTextfield]); 
Reset([@lastNameAccountCreationTextfield]); 
Reset([@firstSocialSecurityDigitsTextfield]); 
Reset([@secondSocialSecurityDigitsTextfield]); 
Reset([@thirdSocialSecurityTextfield]); 
Reset([@dateOfBirthDatepicker]); 
Reset([@firstSecurityQuestionDropdown]); 
Reset([@secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown]); 
Reset([@agreementCheckbox])
 
### d. Create Account Button:

If(!LookUp('[dbo].[Customer]', Username = usernameBasicInformationTextfield.Text, EmailAddress = emailBasicInformationTextfield.Text), ClearCollect(AccountCreation, {Username: usernameBasicInformationTextfield.Text, PasswordField: passwordBasicInformationScreenTextfield.Text, EmailAddress: emailBasicInformationTextfield.Text, SecurityQuestion1: firstSecurityQuestionDropdown.Selected.Result, SecurityAnswer1:firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield.Text, SecurityQuestion2: secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown.Selected.Result, SecurityAnswer2: secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield.Text, MobileNumber: mobileAccountCreationSecurityQuestionsScreenTextfield.Text, FirstName: firstNameAccountCreationTextfield.Text, LastName: lastNameAccountCreationTextfield.Text, SocialSecurityNumber: Concatenate(firstSocialSecurityDigitsTextfield.Text,"-",secondSocialSecurityDigitsTextfield.Text,"-",thirdSocialSecurityTextfield.Text), DateOfBirth: dateOfBirthDatepicker.SelectedDate, TermsAgreement: agreementCheckbox.Text}),LookUp('[dbo].[Customer]', Username = usernameBasicInformationTextfield.Text, EmailAddress = emailBasicInformationTextfield.Text),UpdateContext({AccountExists: true})); If(Connection.Connected,(ForAll(AccountCreation, Patch('[dbo].[Customer]', Defaults('[dbo].[Customer]'),{Username: Username, PasswordField: PasswordField, EmailAddress: EmailAddress, SecurityQuestion1: SecurityQuestion1, SecurityAnswer1:SecurityAnswer1, SecurityQuestion2: SecurityQuestion2, SecurityAnswer2: SecurityAnswer2, MobileNumber: MobileNumber, FirstName: FirstName, LastName: LastName, SocialSecurityNumber:SocialSecurityNumber, DateOfBirth: DateOfBirth, TermsAgreement: TermsAgreement}))));If(Connection.Connected,Navigate([@'Login Screen'],ScreenTransition.Fade));If(!Connection.Connected,Navigate([@'Account Creation Connection Timer Screen'],ScreenTransition.Fade));Reset([@passwordLoginScreenTextfield]); Reset([@usernameLoginScreenTextfield]); 
Reset([@findEmailForgotUsernameScreenTextfield]); 
Reset([@firstSecurityQuestionAnswerTextfield]); 
Reset([@secondSecurityQuestionAnswerTextfield]); 
Reset([@newPasswordInputTextfield]); 
Reset([@emailBasicInformationTextfield]); 
Reset([@usernameBasicInformationTextfield]); 
Reset([@passwordBasicInformationScreenTextfield]); 
Reset([@confirmPasswordBasicInformationScreenTextfield]); 
Reset([@firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield]); 
Reset([@mobileAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@firstNameAccountCreationTextfield]); 
Reset([@lastNameAccountCreationTextfield]); 
Reset([@firstSocialSecurityDigitsTextfield]); 
Reset([@secondSocialSecurityDigitsTextfield]); 
Reset([@thirdSocialSecurityTextfield]); 
Reset([@dateOfBirthDatepicker]); 
Reset([@firstSecurityQuestionDropdown]); 
Reset([@secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown]); 
Reset([@agreementCheckbox])

# 6. Forgot Username Screen:

## On this screen we see a textfield, cancel button, next button:
 
### a. Cancel Button, Onselect Property:

Back(ScreenTransition.Fade)
 
### b. Next Button:

LookUp('[dbo].[Customer]', EmailAddress = findEmailForgotUsernameScreenTextfield.Text, Navigate([@'Account Security Questions Validation'], ScreenTransition.Fade))

# 7. Account Security Questions Validation:

## Screen that generates the questions depending on the user trying to reset the password, if the questions are the same in the database, it allows the user to reset the password on the next page:
 
### a. firstSecurityQuestionValidationTextfield, text property:

LookUp('[dbo].[Customer]', EmailAddress = findEmailForgotUsernameScreenTextfield.Text,SecurityQuestion1)
 
### b. secondSecurityQuestionValidationTextfield, text property:

LookUp('[dbo].[Customer]', EmailAddress = findEmailForgotUsernameScreenTextfield.Text,SecurityQuestion2)
 
### c. Screen, OnVisible Property:

ClearCollect(Security_Questions, {Question:"Choose"}, {Question:"What city were you born?"},{Question:"In what city was your first job?"},{Question:"What is the middle name of your youngest child?"}, {Question:"What was the make and model of your first car?"}, {Question:"What was your high school mascot?"}, {Question:"What is your oldest sibling's birthday month and year?"}, {Question:"What was the last name of your 3rd grade teacher?"}, {Question:"In what city does your nearest sibling live?"}, {Question:"What street did you live on in 6th grade?"}, {Question:"What was the name of your first pet?"}, {Question:"What is your favorite vacation spot?"}, {Question:"What was your childhood nickname?"})
 
### d. Boton Next, OnSelect Property:

If(LookUp('[dbo].[Customer]', SecurityAnswer1 = firstSecurityQuestionAnswerTextfield.Text, SecurityAnswer2 = secondSecurityQuestionAnswerTextfield.Text), Navigate([@'Reset New Password Screen'], ScreenTransition.Fade))
 
### e. Boton de Cancel, OnSelect Property:

Back(ScreenTransition.Fade)

# 8. Reset New Password Screen:

## A textfield to put the new password, a cancel button and a reset password button:
 
### a. Reset New Password Button, OnSelect Property:

If(!IsBlank(Patch('[dbo].[Customer]',First(Filter('[dbo].[Customer]', EmailAddress = findEmailForgotUsernameScreenTextfield.Text)),{PasswordField: newPasswordInputTextfield.Text})), Navigate([@'Login Screen'],ScreenTransition.Fade));Reset([@passwordLoginScreenTextfield]); Reset([@usernameLoginScreenTextfield]); 
Reset([@findEmailForgotUsernameScreenTextfield]); 
Reset([@firstSecurityQuestionAnswerTextfield]); 
Reset([@secondSecurityQuestionAnswerTextfield]); 
Reset([@newPasswordInputTextfield]); 
Reset([@emailBasicInformationTextfield]); 
Reset([@usernameBasicInformationTextfield]); 
Reset([@passwordBasicInformationScreenTextfield]); 
Reset([@confirmPasswordBasicInformationScreenTextfield]); 
Reset([@firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield]); 
Reset([@mobileAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@firstNameAccountCreationTextfield]); 
Reset([@lastNameAccountCreationTextfield]); 
Reset([@firstSocialSecurityDigitsTextfield]); 
Reset([@secondSocialSecurityDigitsTextfield]); 
Reset([@thirdSocialSecurityTextfield]); 
Reset([@dateOfBirthDatepicker]); 
Reset([@firstSecurityQuestionDropdown]); 
Reset([@secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown]); 
Reset([@agreementCheckbox])
 
### b. Boton Cancel, OnSelect Property:

Navigate([@'Login Screen'],ScreenTransition.Fade); Reset([@passwordLoginScreenTextfield]); Reset([@usernameLoginScreenTextfield]); 
Reset([@findEmailForgotUsernameScreenTextfield]); 
Reset([@firstSecurityQuestionAnswerTextfield]); 
Reset([@secondSecurityQuestionAnswerTextfield]); 
Reset([@newPasswordInputTextfield]); 
Reset([@emailBasicInformationTextfield]); 
Reset([@usernameBasicInformationTextfield]); 
Reset([@passwordBasicInformationScreenTextfield]); 
Reset([@confirmPasswordBasicInformationScreenTextfield]); 
Reset([@firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield]); 
Reset([@mobileAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@firstNameAccountCreationTextfield]); 
Reset([@lastNameAccountCreationTextfield]); 
Reset([@firstSocialSecurityDigitsTextfield]); 
Reset([@secondSocialSecurityDigitsTextfield]); 
Reset([@thirdSocialSecurityTextfield]); 
Reset([@dateOfBirthDatepicker]); 
Reset([@firstSecurityQuestionDropdown]); 
Reset([@secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown]); 
Reset([@agreementCheckbox])

# 9. Account Creation Connection Timer Screen:

## Screen with a timer, button to retry a patch and save button locally:
 
### a. Screen OnVisible Property:

UpdateContext({ResetTimer:false});UpdateContext({StartTimer:false})
 
### b. Timer control:

#### i. OnTimerEnd:

If(Connection.Connected,
      ForAll(AccountCreation, Patch('[dbo].[Customer]', Defaults('[dbo].[Customer]'),{Username: Username, PasswordField: PasswordField, EmailAddress: EmailAddress, SecurityQuestion1: SecurityQuestion1, SecurityAnswer1:SecurityAnswer1, SecurityQuestion2: SecurityQuestion2, SecurityAnswer2: SecurityAnswer2, MobileNumber: MobileNumber, FirstName: FirstName, LastName: LastName, SocialSecurityNumber:SocialSecurityNumber, DateOfBirth: DateOfBirth, TermsAgreement: TermsAgreement}))); If(Connection.Connected,Clear(AccountCreation)); If(Connection.Connected,Navigate([@'Login Screen'],ScreenTransition.Fade))

#### ii. Start:

TimerStart

#### iii. AutoStart:

true

#### iv. Repeat:

true

#### v. Duration:

20000
 
### c. Retry Button: OnSelect Property:

UpdateContext({ResetTimer:false});UpdateContext({ResetTimer:true});UpdateContext({StartTimer: false});UpdateContext({StartTimer: true});If(Connection.Connected,
      ForAll(AccountCreation, Patch('[dbo].[Customer]', Defaults('[dbo].[Customer]'),{Username: Username, PasswordField: PasswordField, EmailAddress: EmailAddress, SecurityQuestion1: SecurityQuestion1, SecurityAnswer1:SecurityAnswer1, SecurityQuestion2: SecurityQuestion2, SecurityAnswer2: SecurityAnswer2, MobileNumber: MobileNumber, FirstName: FirstName, LastName: LastName, SocialSecurityNumber:SocialSecurityNumber, DateOfBirth: DateOfBirth, TermsAgreement: TermsAgreement}))); If(Connection.Connected,Clear(AccountCreation)); If(Connection.Connected,Navigate([@'Login Screen'],ScreenTransition.Fade))
 
### e. Import Control Button:

#### i. OnSelect:

Clear(AccountCreation);Reset([@passwordLoginScreenTextfield]); Reset([@usernameLoginScreenTextfield]); 
Reset([@findEmailForgotUsernameScreenTextfield]); 
Reset([@firstSecurityQuestionAnswerTextfield]); 
Reset([@secondSecurityQuestionAnswerTextfield]); 
Reset([@newPasswordInputTextfield]); 
Reset([@emailBasicInformationTextfield]); 
Reset([@usernameBasicInformationTextfield]); 
Reset([@passwordBasicInformationScreenTextfield]); 
Reset([@confirmPasswordBasicInformationScreenTextfield]); 
Reset([@firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield]); 
Reset([@mobileAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@firstNameAccountCreationTextfield]); 
Reset([@lastNameAccountCreationTextfield]); 
Reset([@firstSocialSecurityDigitsTextfield]); 
Reset([@secondSocialSecurityDigitsTextfield]); 
Reset([@thirdSocialSecurityTextfield]); 
Reset([@dateOfBirthDatepicker]); 
Reset([@firstSecurityQuestionDropdown]); 
Reset([@secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown]); 
Reset([@agreementCheckbox]);
Navigate([@'Login Screen'],ScreenTransition.Fade)

#### ii. Data:

AccountCreation

# 10. Account Creation Imported Data Connection Timer Screen

## Screen with a timer, button to retry a Patch and button to cancel:

### a. Screen OnVisible Property:

UpdateContext({ResetTimer:false});UpdateContext({StartTimer:false})
 
### b. Timer control:

#### i. OnTimerEnd:

If(Connection.Connected,
      ForAll(ImportedAccountCreation, Patch('[dbo].[Customer]', Defaults('[dbo].[Customer]'),{Username: Username, PasswordField: PasswordField, EmailAddress: EmailAddress, SecurityQuestion1: SecurityQuestion1, SecurityAnswer1:SecurityAnswer1, SecurityQuestion2: SecurityQuestion2, SecurityAnswer2: SecurityAnswer2, MobileNumber: MobileNumber, FirstName: FirstName, LastName: LastName, SocialSecurityNumber:SocialSecurityNumber, DateOfBirth: DateOfBirth, TermsAgreement: TermsAgreement}))); If(Connection.Connected,Clear(ImportedAccountCreation)); If(Connection.Connected,Navigate([@'Login Screen'],ScreenTransition.Fade))

#### ii. Start:

TimerStart

#### iii. AutoStart:

true

#### iv. Repeat:

true

#### v. Duration:

20000
 
### c. Retry Button, OnSelect Property:

UpdateContext({ResetTimer:false});UpdateContext({ResetTimer:true});UpdateContext({StartTimer: false});UpdateContext({StartTimer: true});If(Connection.Connected,
      ForAll(ImportedAccountCreation, Patch('[dbo].[Customer]', Defaults('[dbo].[Customer]'),{Username: Username, PasswordField: PasswordField, EmailAddress: EmailAddress, SecurityQuestion1: SecurityQuestion1, SecurityAnswer1:SecurityAnswer1, SecurityQuestion2: SecurityQuestion2, SecurityAnswer2: SecurityAnswer2, MobileNumber: MobileNumber, FirstName: FirstName, LastName: LastName, SocialSecurityNumber:SocialSecurityNumber, DateOfBirth: DateOfBirth, TermsAgreement: TermsAgreement}))); If(Connection.Connected,Clear(ImportedAccountCreation)); If(Connection.Connected,Navigate([@'Login Screen'],ScreenTransition.Fade))
 
### d. Cancel Button, Onselect Property:

Clear(ImportedAccountCreation);Navigate([@'Launch Screen'],ScreenTransition.Fade)

# 11. Main Screen:

## A label that shows the user logged in, a label that presents the result of a formula that subtracts the total of deposits and the total of withdrawals, a button that deposits, a button that retires, a button that executes clear of what is written in the textfields and a button that gives exit of the application to the user:
 
### a. Name Label, Text Property:

usernameLoginScreenTextfield.Text
 
### b. Total Balance Label, Text Property:

TotalDeposit - TotalWithdrawal
 
### c. Deposit Button, OnSelect Property:

Patch('[dbo].[Transactions]',{Deposit: depositMainScreenTextfield.Text, TransactionDate: Now(), Username: usernameLoginScreenTextfield.Text, AccountType:accountTypeDropdown.Selected.Result});Reset(depositMainScreenTextfield);Reset(withdrawalMainScreenTextfield);UpdateContext({TotalDeposit: Sum(Filter('[dbo].[Transactions]',accountTypeDropdown.Selected.Result = AccountType),Deposit)}); UpdateContext({TotalWithdrawal: Sum(Filter('[dbo].[Transactions]',accountTypeDropdown.Selected.Result = AccountType),Withdrawal)})
 
### d. Withdrawal Button, OnSelect Property:

Patch('[dbo].[Transactions]',{Withdrawal: withdrawalMainScreenTextfield.Text, TransactionDate: Now(), Username: usernameLoginScreenTextfield.Text, AccountType:accountTypeDropdown.Selected.Result});Reset(depositMainScreenTextfield);Reset(withdrawalMainScreenTextfield);UpdateContext({TotalDeposit: Sum(Filter('[dbo].[Transactions]',accountTypeDropdown.Selected.Result = AccountType),Deposit)}); UpdateContext({TotalWithdrawal: Sum(Filter('[dbo].[Transactions]',accountTypeDropdown.Selected.Result = AccountType),Withdrawal)})
 
### e. Clear Button, OnSelect Property:

Reset(depositMainScreenTextfield);Reset(withdrawalMainScreenTextfield)
 
### f. Exit Button, OnSelect Property:

Navigate([@'Launch Screen'],ScreenTransition.Fade); Reset([@passwordLoginScreenTextfield]); Reset([@usernameLoginScreenTextfield]); 
Reset([@findEmailForgotUsernameScreenTextfield]); 
Reset([@firstSecurityQuestionAnswerTextfield]); 
Reset([@secondSecurityQuestionAnswerTextfield]); 
Reset([@newPasswordInputTextfield]); 
Reset([@emailBasicInformationTextfield]); 
Reset([@usernameBasicInformationTextfield]); 
Reset([@passwordBasicInformationScreenTextfield]); 
Reset([@confirmPasswordBasicInformationScreenTextfield]); 
Reset([@firstSecurityAnswerAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@secondSecurityAnswerAccountCreationsSecurityQuestionsScreenTextfield]); 
Reset([@mobileAccountCreationSecurityQuestionsScreenTextfield]); 
Reset([@firstNameAccountCreationTextfield]); 
Reset([@lastNameAccountCreationTextfield]); 
Reset([@firstSocialSecurityDigitsTextfield]); 
Reset([@secondSocialSecurityDigitsTextfield]); 
Reset([@thirdSocialSecurityTextfield]); 
Reset([@dateOfBirthDatepicker]); 
Reset([@firstSecurityQuestionDropdown]); 
Reset([@secondSecurityQuestionAccountCreationSecurityQuestionsScreenDropdown]); 
Reset([@agreementCheckbox])
 
### g. Screen, OnVisible Property:

ClearCollect(Account_Types, {Type:"Checking"}, {Type:"Savings"}); UpdateContext({TotalDeposit: Sum(Filter('[dbo].[Transactions]',accountTypeDropdown.Selected.Result = AccountType),Deposit)}); UpdateContext({TotalWithdrawal: Sum(Filter('[dbo].[Transactions]',accountTypeDropdown.Selected.Result = AccountType),Withdrawal)})
 
### h. Dropdown Menu, Items Property:

Distinct(Account_Types, Type)
