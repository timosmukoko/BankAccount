CA Assignment – Test Driven Development (TDD)
+++++++++++++++++++++++++++++++++++++++++++++

There are at least three behaviors that need to be checked:
	-The method throws an ArgumentOutOfRangeException if the debit amount is greater than the balance. The test method fails.
	-The method throws an ArgumentOutOfRangeException if the debit amount is less than zero. The test method fails.
	-If the debit amount is valid, the method subtracts the debit amount from the account balance. The test method pass

The first test verifies that a valid amount (that is, one that is less than the account balance and greater than zero) withdraws the correct amount from the account. Add the following method to that BankAccountTests class:
The method is straightforward: it sets up a new BankAccount object with a beginning balance, and then withdraws a valid amount. It uses the AreEqual method to verify that the ending balance is as expected.
The test result contains a message that describes the failure. For the AreEqual method, the message displays what was expected (the Expected<value> parameter) and what was actually received (the Actual<value> parameter). You expected the balance to decrease, but instead it increased by the amount of the withdrawal.
The unit test has uncovered a bug: the amount of the withdrawal is added to the account balance when it should be subtracted.

====== Correct the bug ====== 
To correct the error, replace the line: 
m_balance += amount;
to
m_balance -= amount;

Assume there's a bug in the method under test, and the Debit method doesn't even throw an ArgumentOutOfRangeException, nevermind output the correct message with the exception. Currently, the test method doesn't handle this case. If the debitAmount value is valid (that is, less than the balance but greater than zero), no exception is caught, so the assert never fires. Yet, the test method passes. This is not good, because you want the test method to fail if no exception is thrown.
This is a bug in the test method. To resolve the issue, add an Fail assert at the end of the test method to handle the case where no exception is thrown.
But rerunning the test shows that the test now fails if the correct exception is caught. The catchblock catches the exception, but the method continues to execute and it fails at the new Fail assert. To resolve this problem, add a return statement after the StringAssert in the catch block. Rerunning the test confirms that you've fixed this problem.

