A VPC peering connection in AWS allows you to route traffic between two Virtual Private Clouds (VPCs). This is useful when you want to allow different VPCs to communicate with each other, whether they're in the same AWS account or in different accounts. Here’s an example scenario and steps for setting up a VPC peering connection.
Example Scenario:

    VPC 1 (VPC-A):
        CIDR Block: 10.0.0.0/16
        Region: US East (N. Virginia)
    VPC 2 (VPC-B):
        CIDR Block: 192.168.0.0/16
        Region: US West (N. California)

You want to allow instances in VPC-A to communicate with instances in VPC-B via a peering connection.
Steps for Creating a VPC Peering Connection:
1. Create VPCs (if not already created)

You can create the VPCs using the AWS Management Console, AWS CLI, or CloudFormation. Here, we'll assume that VPC-A and VPC-B already exist with the CIDR blocks mentioned in the example.
2. Create the Peering Connection Request (VPC-A to VPC-B)

    Go to the VPC Dashboard in the AWS Management Console.

    Under Peering Connections, click on Create Peering Connection.

    Choose the following:
        Peering Connection Name: VPC-A-to-VPC-B
        Requester VPC: Select VPC-A (the VPC from which you are creating the peering connection).
        Accepter VPC: Select VPC-B (the VPC that will accept the peering connection).
        Peering Connection Type: Choose Inter-Region (since the VPCs are in different regions).
        Route Propagation: You can enable route propagation later for automatic route updates.

    Click Create Peering Connection.

3. Accept the Peering Connection (from VPC-B)

    Go to the Peering Connections page in the VPC Dashboard.
    Find the Pending Acceptance status for your peering connection (VPC-A-to-VPC-B).
    Select the peering connection and click Actions → Accept Request.
    Confirm the acceptance.

4. Update Route Tables in Both VPCs

Now that the peering connection has been established, you need to update the route tables for both VPCs so they know how to reach the other VPC’s CIDR block.
For VPC-A:

    Go to the Route Tables section in the VPC Dashboard.
    Select the route table associated with the subnets in VPC-A.
    Click Edit routes → Add route.
    In the Destination field, enter the CIDR block of VPC-B: 192.168.0.0/16.
    In the Target field, select the peering connection (VPC-A-to-VPC-B).
    Save the route.

For VPC-B:

    Go to the Route Tables section in the VPC Dashboard.
    Select the route table associated with the subnets in VPC-B.
    Click Edit routes → Add route.
    In the Destination field, enter the CIDR block of VPC-A: 10.0.0.0/16.
    In the Target field, select the peering connection (VPC-A-to-VPC-B).
    Save the route.

5. Update Security Groups

For instances to communicate across the VPC peering connection, you need to ensure the correct security group settings.

    Go to the Security Groups section in the VPC Dashboard.
    Modify the Security Group associated with instances in VPC-A to allow inbound traffic from the CIDR block of VPC-B (192.168.0.0/16).
        For example, allow TCP traffic on port 80 (HTTP) or 22 (SSH) depending on your needs.
    Modify the Security Group associated with instances in VPC-B to allow inbound traffic from the CIDR block of VPC-A (10.0.0.0/16).

6. Test the Peering Connection

Once the routes and security groups are updated, you can test the connection:

    Launch an EC2 instance in each VPC (e.g., instance-A in VPC-A and instance-B in VPC-B).
    From instance-A, try to ping instance-B using its private IP.
        If the ping succeeds, the peering connection is working.
    From instance-B, try to ping instance-A similarly.
