# 3-layer-Arc

![3-Layer-Arc](https://github.com/partho-dev/3-layer-Arc/assets/150241170/a1cd6620-df23-4228-9f6d-e580ba15c83d)

It is very essential to desig the architecture of the infrastructure where the application would be hosted and run.
The main objective 
1. Scalability
2. Durability
3. Security
4. Decouple the components

- In any application, there could be 3 very essential components
* `Front-End` (UI) - Which is customer facing and it can be accesible through ports like `80` or port `443` for secure connection between the user & the application
    - `UI` or Front End is developed using the **HTML**, **CSS** & various **JS libraries** like Anngular or React etc
    - Even mobile apps are also FE which can be developed using native tools like Kotlin/Java for Android & Swift/UI for iOS
    - Mobile app can also be developed using cross-platform language like React Native, Flutter etc
* The request received by the UI on certain `API-endpoint`, should need to be processed by an `API server`, which should only have access from the UI.
    - Note: The API Server should not have any access from open internet over port 80 or 443.
    - The API server can be developed using `Node-Express`, `PHP-Laraval`, `Python dJango` etc
* Onnce the API server receives the request from FE, it would need to communicate with `Database` to process the response for the request made and give the response back to UI.
    - Note : Here, the Database should only be configured to be communicated by the API server alone.

So, we need to isolate these components through a `logical network` boundaries.
- The UI which is public facing and receives the traffic througg port 80 or 443 can be kept in Public facing network
- For AWS, they are called `Public subnet`, whose route table is configures to connect with internet through internet Gateway.
- The API server should be in another `isolated` network and it should be kept in a `private network` and its route table should be configured to have access only within its VPC, 
    - There is no internet gateway attached to private network (Private subnet)
    - The resources in that private network can further be controlled to have granular access to & from through security group.

- The Database should also be in a private subnet and its security group should controll the traffic to be accessible from the private servers belonging to private subnnet.

