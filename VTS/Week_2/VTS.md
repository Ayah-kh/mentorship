## Task 1 - UI

### Employee Request Table View
![UI- Employee1.png](UI- Employee1.png)

### Employee Request Vacation Table
![UI- Employee.png](UI- Employee.png)

### Mangar Table View
![UI- Manager.png](UI- Manager.png)

## Add new Status with minimum change

To be able to add a table with minimum change , adding status and the action that lead to that status is configurable.
To be able to achieve that two different component must be added:
1. State Configuration UI
2. State Configuration Controller, Service, Repository

**Suggested State Configuration Table Design**

![stateConfigTable.drawio.png](stateConfigTable.drawio.png)

##  pseudo-code 



```
public void performAction(String action, EmployeeRequestDto dto) {
    String user = getCurrentUserFromJwt();
    stateConfigService.validateAction(action).orElseThrowException;
    String status = stateConfigService.getStatus(user, action);
    EmployeeRequest req = Mapper.toEntity(dto);
    req.setStatus()
    employeeRequestRepo.save(req);
 ```

## state machine of the request
![state_machine.drawio.png](state_machine.drawio.png)

## sequence diagram of the request
![Seq- Employee Request Vacation.png](Seq- Employee Request Vacation.png)

![Seq- Employee Edit Vacation Request.png](Seq- Employee Edit Vacation Request.png)

![Seq- Employee Cancel Vacation Request.png](Seq- Employee Cancel Vacation Request.png)

![Seq- Manager Approve Vacation.png](Seq- Manager Approve Vacation.png)


