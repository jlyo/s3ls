s3ls writes a listing of S3 buckets and objects.

Dependencies:
	python3 (https://www.python.org/)
	boto3 (https://aws.amazon.com/sdk-for-python/)

Installation:
	populate AWS credentials in ~/.aws/credentials with the following
  template:
	[default]
	aws_access_key_id =
	aws_secret_access_key =

Usage: s3ls [ -hkmgr ] [ -N limit ] [ bucket ]
    -h: show this help
    -k: report sizes in kilobytes
    -m: report sizes in megabytes
    -g: report sizes in gigabytes
    -N: list up to limit number of files
    -r: reverse sorted order
    bucket: a regex matching bucket names

s3ls writes a list of tab separated values for Amazon S3 buckets and
objects to standard output.  s3ls first lists all buckets visible
to s3ls and matching the "bucket" command line option, if provided,
in no particular order.  Next, s3ls lists all objects within the
aforementioned buckets, sorted by last modification time. The -N
option can be used to limit s3ls's object output.

Names containing a tab character, newline, or backslash are escaped
into their three digit octal representation, preceded by a backslash,
i.e. \nnn.

The columns for objects are:
  bucket name
  object name
  time of last modification in RFC822 format
  size in bytes (unless -k, -m, or -g command line options are given)

The columns for buckets are:
  name
  empty
  timestamp of the last modification of the most recently updated object
  sum of the sizes for all objects in the bucket
	time of bucket creation
  number of objects contained in the bucket

Bugs:
	-k, -m, -g, formatting isn't very pretty
  unspecified regex dialect
  code hackily adds anchors when compiling the bucket regex
