import ballerina/http;
import ballerina/graphql;

public function main() {
    http:Client client = check new http:Client("http://localhost:8080/graphql");

    // Define GraphQL queries and mutations to interact with the server.
    string getEmployeesAndDepartmentsQuery = `{
        getEmployeesAndDepartments {
            ... on Employee {
                user {
                    firstName
                    lastName
                }
                department {
                    name
                }
                individualKPIs {
                    name
                }
            }
            ... on Department {
                name
                objectives
                kpis {
                    name
                }
            }
        }
    }`;

    string updateEmployeeKPIMutation = `mutation($empId: Int!, $kpiName: String!, $score: Float!) {
        updateEmployeeKPI(empId: $empId, kpiName: $kpiName, score: $score) {
            user {
                firstName
                lastName
            }
            individualKPIs {
                name
            }
        }
    }`;

    // Define variables for query/mutation parameters.
    json queryVariables = {
        "empId": 1,
        "kpiName": "Performance",
        "score": 4.5
    };

    // Use the client to send queries and mutations to the server.
    var response = client->post("/graphql", getEmployeesAndDepartmentsQuery, queryVariables);

    match response {
        http:Response resp => {
            io:println("Response: " + resp.getStringPayload());
        }
        error err => {
            io:println("Error: " + err.message);
        }
    }

    // You can also send mutations in a similar way using updateEmployeeKPIMutation.
}
