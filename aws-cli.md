## Filtering

`--filter` requres `Name=name-of-arg,Values=val1,val2,etc` formatting

http://docs.aws.amazon.com/cli/latest/userguide/cli-using-param.html

    aws ec2 describe-instances --filters \
        "Name=instance-type,Values=t2.micro,m1.medium" \
        "Name=availability-zone,Values=us-west-2c"

## Controlling output format with query

http://docs.aws.amazon.com/cli/latest/userguide/controlling-output.html

    ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-76863d13" \
        --query "Subnets[*].[AvailabilityZone, SubnetId, VpcId]"

## Find your account id from the cli

    aws sts get-caller-identity
    
    {
        "Account": "1234567000", 
        "UserId": "ABCJOALKJFSDLFSDF", 
        "Arn": "arn:aws:iam::1234567000:user/brianz"
    }
