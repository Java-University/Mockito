# Mockito

http://bigdataconsultants.blogspot.com/2015/01/interview-questions-about-mockito.html

The abiding principle of Mocking framework is that each class should be independently testable and should not depend on other bean. So, if we have a service class, we should have a serviceTest to test the code in that class. If there is dependency on any other class, then that class should be mocked and injected in the serviceTest.
This is the reason why, in TEST class, it is acceptable to repeat the code.




What is Mockito? 
Mockito allows creation of mock object for the purpose of Test Driven Development and Behavior Driven development. Unlike creating actual object, Mockito allows creation of fake object (external dependencies) which allows it to give consistent results to a given invocation.

Why do we need Mockito? What are the advantages?
Mockito differentiates itself from the other testing framework by removing the expectation beforehand. So, by doing this, it reduces the coupling. Most of the testing framework works on the "expect-run-verify". Mockito allows it to make it "run-verify" framework. Mockito also provides annotation which allows to reduce the boilerplate code.

Can you explain a MOCKITO framework?
In Mockito, you always check a particular class. The dependency in that class is injected using mock object. So, for example, if you have service class, then the Dao class are injected as a mockDao. This enables us to check only the method of that given service class and whether they are performing as expected or not. 

For example, suppose, service class has an updateObject Method. That update method is depend on Dao1, Dao2. Here the objective is to test only the updateObject method and not the Dao1 and Dao2. So, we can create a mockDao and return a mock object. This object is not the one which is in the database but is custom made. It only tests whether the updates are happening as expected or not. The syntax to create a Mock object is as follows:
private static LedgerBook mockLedgerBook;
In the setup(), you create the mock object
setup(){
mockLedgerBook = Mockito.mock(LedgeBookDao.class);
}
In the test method, you call this mockLedgerBook as follows:
LedgerBook ledgerBook = new LedgerBook();
ledgerBook.setName("default");
Mockito.when(mockLedgerBook.findBookById(Mockito.anyLong()).thenReturn(ledgerBook);


What are the different annotation that is used in Mockito?

What is the version you used for Mockito framework?
I used 1.9.5 version of Mockito.

How do you create a mockDB object in Mockito?
We need to create the mock object and need to pass the invocation. We must override the method in the actual DB with the method over here and pass the response object.
 Mockito.when(mockObjectDao.find((Guid) Mockito.anyObject())).thenAnswer(new Answer<responseObject>() {
            @Override
            public responseObject answer(InvocationOnMock invocation) throws Throwable {
                Guid responseObjectID = (Guid) invocation.getArguments()[0];
                responseObject responseDbObject = new responseObject();
                responseDbObject.setresponseObjectId(responseObjectID);
                responseObjectLink responseObjectLink = new responseObjectLink();
                responseObjectLink.setLedgerBookId(Guid.createGuid());
                responseObjectLink.setresponseObjectId(responseObjectID);
                responseObjectLink.setLedgerObjectId(Guid.createGuid());
                responseDbObject.getresponseObjectLinks().add(responseObjectLink);
                for (Contact sourceContact : responseObjectDTO.getSourceContacts()) {
                    if (!sourceContact.getObjectId().equals(responseObjectID)) {
                        responseObjectLink = new responseObjectLink();
                        responseObjectLink.setLedgerBookId(sourceContact.getAddressBookId());
                        responseObjectLink.setresponseObjectId(responseObjectID);
                        responseObjectLink.setLedgerObjectId(sourceContact.getObjectId());
                        responseDbObject.getresponseObjectLinks().add(responseObjectLink);
                    }
                }
                return responseDbObject;
            }

        });

source:
http://martinfowler.com/articles/mocksArentStubs.html
http://searchsoftwarequality.techtarget.com/tip/Using-JMock-in-test-driven-development
