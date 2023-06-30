# Connect-EC2-instance-with-EBS-using-boto3

1: Install Boto3

pip install boto3

2. Configure AWS Credentials

aws configure

3. Import Boto3 and Establish a Session

import boto3

session = boto3.Session()

4. Create an SSM Client

ssm_client = session.client('ssm')

5. Retrieve Instance IDs
6. Send Command to Connect Instances

response = ssm_client.send_command(
    InstanceIds=instance_ids,
    DocumentName='AWS-RunShellScript',
    Parameters={'commands': ['echo "Hello, SSM!"']}
)

7. Check Command Execution Status

command_id = response['Command']['CommandId']

command_invocation = ssm_client.get_command_invocation(
    CommandId=command_id,
    InstanceId=instance_ids[0]  # Specify one of the instance IDs for the command
)

status = command_invocation['Status']
output = command_invocation['StandardOutputContent']
