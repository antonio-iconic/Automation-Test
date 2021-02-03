[Screen Shot 2021-02-03 at 12.54.07 PM.png](https://trello-attachments.s3.amazonaws.com/6012ec6cd7a49a3ff40475f0/6012ec6dd7a49a3ff4047738/2a6c923ad5227c5ce89c657440e07081/Screen_Shot_2021-02-03_at_12.54.07_PM.png) 

// Pre-request script
const email = pm.variables.replaceIn("{{$randomEmail}}");
const userName = pm.variables.replaceIn("{{$randomUserName}}");
const firstName = pm.variables.replaceIn("{{$randomFirstName}}");
const lastName = pm.variables.replaceIn("{{$randomLastName}}");
const phone = pm.variables.replaceIn("{{$randomPhoneNumber}}");
pm.environment.set("email", email);
pm.environment.set("id", (()=>Math.ceil(Math.random() * 10000 + 1))());
pm.environment.set("userName", userName);
pm.environment.set("firstName", firstName);
pm.environment.set("lastName", lastName);
pm.environment.set("password", "asd.456");
pm.environment.set("phone", phone);

// Tests

pm.test("A. Status code is 200", function () {
    const response = pm.response;
    response.to.have.status(200);
});

pm.test("B. Message : User ID Ok", function() {
    const response = pm.response;
    const body = response.json();
    pm.expect(body).has.property("message");
    console.log(body)
    pm.environment.set("id", Number(body.message))
});
