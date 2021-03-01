# Java Technical Case
As soon as recriter talk to me, I did receive a link to complete the java technical case in [Qualified.io](https://www.qualified.io/assess/5bd1b12f82f35e000fb6e517/review?invite=mZCWebxYCohWbA).

The following are 3 challeges, I have been asked to complete, And Suprisingly there was no time limit, But after 55 min, the clock was showing warning/yello color on it.
> Note: Please read instructions very carefully about timings. Because during the test I thought I have only 55 min and it was kind of disturing my mind whether or not i will be able to solve all 3 challeges withing 55 min. Luckily it was not auto submitted, instead the timer got different color.

## Challegenge 1: DNS Strand

It was little easy question, the inout is the one DNS strand, we need to return another DNA strand by replacing the following:
1. A's base is T and vise versa
2. C's base is G and vise versa

The following is the complete solution passed all test cases.
```java
class Challenge {
    public static String dnaComplement(String dna) {

       if(dna.isEmpty()) {
           return "";
       }
       StringBuilder otherDNAStrand = new StringBuilder();
       for (int i = 0 ; i < dna.length(); i++) {
           char currentChar = dna.charAt(i);
           otherBase(otherDNAStrand, currentChar);

       }
        return otherDNAStrand.toString();
    }

    private static void otherBase(StringBuilder otherDNAStrand, char currentChar) {
        switch (currentChar) {
            case 'A':
                otherDNAStrand.append("T");
                break;
            case 'T':
                otherDNAStrand.append("A");
                break;
            case 'C':
                otherDNAStrand.append("G");
                break;
            default:
                otherDNAStrand.append("C");

        }
    }
}
```

## Challege 2: Java Stream API
Given: list of customer and target minAge
we need to return list of customer (sorted by last name and then first name in the format of **Lastname, FirstName**) who are eligible to buy a product. The given target minAge is the cretiria to to decide whether or not the cusotmer is eligible.

The following is the following which I had submitted, But later I realised that its wrong.
```java
public class Challenge {

    public static List<String> getAllNames(List<Customer> customers, int minAge) {
        System.out.println(minAge);
        System.out.println(customers.size());
        customers.stream().forEach( c -> {
            System.out.println(c.getAge() + " " +c.getLastName() + " " + c.getFirstName());
        });
        Comparator<Customer> compareByName = Comparator
                .comparing(Customer::getFirstName)
                .thenComparing(Customer::getLastName);
        
        return customers
                .stream()
                .filter(customer -> customer.getAge() >= minAge)
                .sorted(compareByName)
                .map( customer -> customer.getLastName() + ", " + customer.getFirstName())
                .collect(Collectors.toList());
    }
}
```

> Note: In the above solution I am sorting customer based on the first name and then last name which was wrong and because of it, there were some test cases were faling. be careful while debugging.
> Important: I supposed to be submitted the production grade code: and forot tot remove sout. please care ful with this as well.

## Challege 3: Rest Controller

I needed to write the following two endpoints:
1. /articles - returns all articles
2. /articles/{id} - returns a Articles or empty id the given article is not available

```java
@RestController
public class ArticlesController {
    private final ArticleService service;
    public ArticlesController(ArticleService service) {
        this.service = service;
    }

    @GetMapping("/articles")
    public List<Article> getAllArticles() {
        return this.service.getAll();
    }

    @GetMapping("/articles/{id}")
    public ResponseEntity<Article> getAllArticles(@PathVariable("id") int id) {
        Article article = this.service.findById(id);
        if(article == null) {
            new ResponseEntity<Article>(HttpStatus.NOT_FOUND);
        }
        return new ResponseEntity<Article>(article, HttpStatus.OK);
    }
}
```

the test cases were failing saying its expecting 404 for /article/10, but my code was returning 200.
It challenge for you to find the issue from the above solution.

# Conclusion
I had submitted the solutions in 1:45 hours