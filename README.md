# sneaky_gophish
Hiding GoPhish from the boys in blue! See my blog article linked below for details on all the changes made during compilation of GoPhish before using!

* [Never had a bad day phishing](https://www.sprocketsecurity.com/blog/never-had-a-bad-day-phishing-how-to-set-up-gophish-to-evade-security-controls)


# Why?

GoPhish by default tips your hand to defenders and security solutions. The container here strips those indicators and makes other changes to hopefully evade detection during operations. 

# How?

Getting the container up and running is very simple. 

Run the following one-liner to clone the repository and build the container:

```
git clone https://github.com/puzzlepeaches/sneaky_gophish && \
  cd sneaky_gophish && \
  docker build -t sneaky_gophish .
```


To actually run the container headlessly, run the following command:

```
docker run -itd --name sneaky_gophish -p 3333:3333 -p 80:80 sneaky_gophish
```


Thank god that GoPhish doesn't use a universal default password anymore. To get the admin credentials for the image after running it, issue the following command:

```
docker logs sneaky_gophish | grep password
```


You should now be able to navigate to the GoPhish administrator interface at the URL listed below if you are running this on your workstation:

* [https://localhost:3333](https://localhost:3333)




# Caveats

* This container exposes port 8080 for the phishing page sent to users. This means we aren't using SSL out of the box. We reccomend using a reverse proxy and robust redirect rules to protect your GoPhish instance and thwart defenders.
* The changes to this repository aren't the end all for detection capabilities. There is more here that should be done before using it in a real world engagement.
