String Manipulation and Regular Expressions Assignment
================

##### Assignment Instructions

Complete all questions below. After completing the assignment, knit your
document, and download both your .Rmd and knitted output. Upload your
files for peer review.

For each response, include comments detailing your response and what
each line does. Ensure you test your functions with sufficient test
cases to identify and correct any potential bugs.

##### Required Libraries

Load the stringr library

``` r
library(stringr)
```

##### Question 1.

Use str_c to put `(` before the area codes followed by `)` and a space
followed by the phone number.

``` r
### Answer should be of the form "(703) 5551212" "(863) 1234567" "(404) 7891234" "(202) 4799747"

area_codes <- c(703, 863, 404, 202)
phone_nums <- c(5551212, 1234567, 7891234, 4799747)

str_c("(",area_codes,") ", phone_nums )
```

    ## [1] "(703) 5551212" "(863) 1234567" "(404) 7891234" "(202) 4799747"

##### Question 2.

Create a function that receives a single word as an input. Use
str_length() and str_sub() to extract the middle character from the
string. What will you do if the string has an even number of characters?
Test your function on the strings “hamburger” and “hotdog”

``` r
mid_char <- function(word){
  length <- str_length(word)
  is_even <- length %% 2 == 0
  if(is_even){
    cat(floor(length/2))
    str_sub(word, length/2, length/2+1)
  }else{
    str_sub(word, ceiling(length/2),ceiling(length/2))
  }
}

mid_char("hamburger")
```

    ## [1] "u"

``` r
mid_char("hotdog")
```

    ## 3

    ## [1] "td"

##### Question 3.

How would you match the sequence “’? Note this is a double quote, single
quote, backslash and question mark. Build it up one piece at a time. Use
it to identify that sequence contained in s2 below.

``` r
s <- "\"'\\?"
s2 <- str_c("some stuff",s,"more!")

#writeLines(s)
#writeLines(s2)

str_view(s2, "\"\'\\\\\\?")
```

<div id="htmlwidget-62c7686c7c74bc73f3c2" style="width:960px;height:100%;" class="str_view html-widget"></div>
<script type="application/json" data-for="htmlwidget-62c7686c7c74bc73f3c2">{"x":{"html":"<ul>\n  <li>some stuff<span class='match'>\"'\\?<\/span>more!<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>

##### Question 4.

Using the words provided in stringr::words, create regular expressions
that find all words that:

``` r
# End with "ing" or "ise"
words[str_detect(words,"ing$|ise$")]
```

    ##  [1] "advertise" "bring"     "during"    "evening"   "exercise"  "king"     
    ##  [7] "meaning"   "morning"   "otherwise" "practise"  "raise"     "realise"  
    ## [13] "ring"      "rise"      "sing"      "surprise"  "thing"

``` r
# Do not follow the rule "i before e except after c"
words[!str_detect(words,"[^c]ie")]
```

    ##   [1] "a"           "able"        "about"       "absolute"    "accept"     
    ##   [6] "account"     "across"      "act"         "active"      "actual"     
    ##  [11] "add"         "address"     "admit"       "advertise"   "affect"     
    ##  [16] "afford"      "after"       "afternoon"   "again"       "against"    
    ##  [21] "age"         "agent"       "ago"         "agree"       "air"        
    ##  [26] "all"         "allow"       "almost"      "along"       "already"    
    ##  [31] "alright"     "also"        "although"    "always"      "america"    
    ##  [36] "amount"      "and"         "another"     "answer"      "any"        
    ##  [41] "apart"       "apparent"    "appear"      "apply"       "appoint"    
    ##  [46] "approach"    "appropriate" "area"        "argue"       "arm"        
    ##  [51] "around"      "arrange"     "art"         "as"          "ask"        
    ##  [56] "associate"   "assume"      "at"          "attend"      "authority"  
    ##  [61] "available"   "aware"       "away"        "awful"       "baby"       
    ##  [66] "back"        "bad"         "bag"         "balance"     "ball"       
    ##  [71] "bank"        "bar"         "base"        "basis"       "be"         
    ##  [76] "bear"        "beat"        "beauty"      "because"     "become"     
    ##  [81] "bed"         "before"      "begin"       "behind"      "benefit"    
    ##  [86] "best"        "bet"         "between"     "big"         "bill"       
    ##  [91] "birth"       "bit"         "black"       "bloke"       "blood"      
    ##  [96] "blow"        "blue"        "board"       "boat"        "body"       
    ## [101] "book"        "both"        "bother"      "bottle"      "bottom"     
    ## [106] "box"         "boy"         "break"       "brilliant"   "bring"      
    ## [111] "britain"     "brother"     "budget"      "build"       "bus"        
    ## [116] "business"    "busy"        "but"         "buy"         "by"         
    ## [121] "cake"        "call"        "can"         "car"         "card"       
    ## [126] "care"        "carry"       "case"        "cat"         "catch"      
    ## [131] "cause"       "cent"        "centre"      "certain"     "chair"      
    ## [136] "chairman"    "chance"      "change"      "chap"        "character"  
    ## [141] "charge"      "cheap"       "check"       "child"       "choice"     
    ## [146] "choose"      "Christ"      "Christmas"   "church"      "city"       
    ## [151] "claim"       "class"       "clean"       "clear"       "clock"      
    ## [156] "close"       "closes"      "clothe"      "club"        "coffee"     
    ## [161] "cold"        "colleague"   "collect"     "college"     "colour"     
    ## [166] "come"        "comment"     "commit"      "committee"   "common"     
    ## [171] "community"   "company"     "compare"     "complete"    "compute"    
    ## [176] "concern"     "condition"   "confer"      "consider"    "consult"    
    ## [181] "contact"     "continue"    "contract"    "control"     "converse"   
    ## [186] "cook"        "copy"        "corner"      "correct"     "cost"       
    ## [191] "could"       "council"     "count"       "country"     "county"     
    ## [196] "couple"      "course"      "court"       "cover"       "create"     
    ## [201] "cross"       "cup"         "current"     "cut"         "dad"        
    ## [206] "danger"      "date"        "day"         "dead"        "deal"       
    ## [211] "dear"        "debate"      "decide"      "decision"    "deep"       
    ## [216] "definite"    "degree"      "department"  "depend"      "describe"   
    ## [221] "design"      "detail"      "develop"     "difference"  "difficult"  
    ## [226] "dinner"      "direct"      "discuss"     "district"    "divide"     
    ## [231] "do"          "doctor"      "document"    "dog"         "door"       
    ## [236] "double"      "doubt"       "down"        "draw"        "dress"      
    ## [241] "drink"       "drive"       "drop"        "dry"         "due"        
    ## [246] "during"      "each"        "early"       "east"        "easy"       
    ## [251] "eat"         "economy"     "educate"     "effect"      "egg"        
    ## [256] "eight"       "either"      "elect"       "electric"    "eleven"     
    ## [261] "else"        "employ"      "encourage"   "end"         "engine"     
    ## [266] "english"     "enjoy"       "enough"      "enter"       "environment"
    ## [271] "equal"       "especial"    "europe"      "even"        "evening"    
    ## [276] "ever"        "every"       "evidence"    "exact"       "example"    
    ## [281] "except"      "excuse"      "exercise"    "exist"       "expect"     
    ## [286] "expense"     "explain"     "express"     "extra"       "eye"        
    ## [291] "face"        "fact"        "fair"        "fall"        "family"     
    ## [296] "far"         "farm"        "fast"        "father"      "favour"     
    ## [301] "feed"        "feel"        "few"         "fight"       "figure"     
    ## [306] "file"        "fill"        "film"        "final"       "finance"    
    ## [311] "find"        "fine"        "finish"      "fire"        "first"      
    ## [316] "fish"        "fit"         "five"        "flat"        "floor"      
    ## [321] "fly"         "follow"      "food"        "foot"        "for"        
    ## [326] "force"       "forget"      "form"        "fortune"     "forward"    
    ## [331] "four"        "france"      "free"        "friday"      "from"       
    ## [336] "front"       "full"        "fun"         "function"    "fund"       
    ## [341] "further"     "future"      "game"        "garden"      "gas"        
    ## [346] "general"     "germany"     "get"         "girl"        "give"       
    ## [351] "glass"       "go"          "god"         "good"        "goodbye"    
    ## [356] "govern"      "grand"       "grant"       "great"       "green"      
    ## [361] "ground"      "group"       "grow"        "guess"       "guy"        
    ## [366] "hair"        "half"        "hall"        "hand"        "hang"       
    ## [371] "happen"      "happy"       "hard"        "hate"        "have"       
    ## [376] "he"          "head"        "health"      "hear"        "heart"      
    ## [381] "heat"        "heavy"       "hell"        "help"        "here"       
    ## [386] "high"        "history"     "hit"         "hold"        "holiday"    
    ## [391] "home"        "honest"      "hope"        "horse"       "hospital"   
    ## [396] "hot"         "hour"        "house"       "how"         "however"    
    ## [401] "hullo"       "hundred"     "husband"     "idea"        "identify"   
    ## [406] "if"          "imagine"     "important"   "improve"     "in"         
    ## [411] "include"     "income"      "increase"    "indeed"      "individual" 
    ## [416] "industry"    "inform"      "inside"      "instead"     "insure"     
    ## [421] "interest"    "into"        "introduce"   "invest"      "involve"    
    ## [426] "issue"       "it"          "item"        "jesus"       "job"        
    ## [431] "join"        "judge"       "jump"        "just"        "keep"       
    ## [436] "key"         "kid"         "kill"        "kind"        "king"       
    ## [441] "kitchen"     "knock"       "know"        "labour"      "lad"        
    ## [446] "lady"        "land"        "language"    "large"       "last"       
    ## [451] "late"        "laugh"       "law"         "lay"         "lead"       
    ## [456] "learn"       "leave"       "left"        "leg"         "less"       
    ## [461] "let"         "letter"      "level"       "life"        "light"      
    ## [466] "like"        "likely"      "limit"       "line"        "link"       
    ## [471] "list"        "listen"      "little"      "live"        "load"       
    ## [476] "local"       "lock"        "london"      "long"        "look"       
    ## [481] "lord"        "lose"        "lot"         "love"        "low"        
    ## [486] "luck"        "lunch"       "machine"     "main"        "major"      
    ## [491] "make"        "man"         "manage"      "many"        "mark"       
    ## [496] "market"      "marry"       "match"       "matter"      "may"        
    ## [501] "maybe"       "mean"        "meaning"     "measure"     "meet"       
    ## [506] "member"      "mention"     "middle"      "might"       "mile"       
    ## [511] "milk"        "million"     "mind"        "minister"    "minus"      
    ## [516] "minute"      "miss"        "mister"      "moment"      "monday"     
    ## [521] "money"       "month"       "more"        "morning"     "most"       
    ## [526] "mother"      "motion"      "move"        "mrs"         "much"       
    ## [531] "music"       "must"        "name"        "nation"      "nature"     
    ## [536] "near"        "necessary"   "need"        "never"       "new"        
    ## [541] "news"        "next"        "nice"        "night"       "nine"       
    ## [546] "no"          "non"         "none"        "normal"      "north"      
    ## [551] "not"         "note"        "notice"      "now"         "number"     
    ## [556] "obvious"     "occasion"    "odd"         "of"          "off"        
    ## [561] "offer"       "office"      "often"       "okay"        "old"        
    ## [566] "on"          "once"        "one"         "only"        "open"       
    ## [571] "operate"     "opportunity" "oppose"      "or"          "order"      
    ## [576] "organize"    "original"    "other"       "otherwise"   "ought"      
    ## [581] "out"         "over"        "own"         "pack"        "page"       
    ## [586] "paint"       "pair"        "paper"       "paragraph"   "pardon"     
    ## [591] "parent"      "park"        "part"        "particular"  "party"      
    ## [596] "pass"        "past"        "pay"         "pence"       "pension"    
    ## [601] "people"      "per"         "percent"     "perfect"     "perhaps"    
    ## [606] "period"      "person"      "photograph"  "pick"        "picture"    
    ## [611] "place"       "plan"        "play"        "please"      "plus"       
    ## [616] "point"       "police"      "policy"      "politic"     "poor"       
    ## [621] "position"    "positive"    "possible"    "post"        "pound"      
    ## [626] "power"       "practise"    "prepare"     "present"     "press"      
    ## [631] "pressure"    "presume"     "pretty"      "previous"    "price"      
    ## [636] "print"       "private"     "probable"    "problem"     "proceed"    
    ## [641] "process"     "produce"     "product"     "programme"   "project"    
    ## [646] "proper"      "propose"     "protect"     "provide"     "public"     
    ## [651] "pull"        "purpose"     "push"        "put"         "quality"    
    ## [656] "quarter"     "question"    "quick"       "quid"        "quite"      
    ## [661] "radio"       "rail"        "raise"       "range"       "rate"       
    ## [666] "rather"      "read"        "ready"       "real"        "realise"    
    ## [671] "really"      "reason"      "receive"     "recent"      "reckon"     
    ## [676] "recognize"   "recommend"   "record"      "red"         "reduce"     
    ## [681] "refer"       "regard"      "region"      "relation"    "remember"   
    ## [686] "report"      "represent"   "require"     "research"    "resource"   
    ## [691] "respect"     "responsible" "rest"        "result"      "return"     
    ## [696] "rid"         "right"       "ring"        "rise"        "road"       
    ## [701] "role"        "roll"        "room"        "round"       "rule"       
    ## [706] "run"         "safe"        "sale"        "same"        "saturday"   
    ## [711] "save"        "say"         "scheme"      "school"      "science"    
    ## [716] "score"       "scotland"    "seat"        "second"      "secretary"  
    ## [721] "section"     "secure"      "see"         "seem"        "self"       
    ## [726] "sell"        "send"        "sense"       "separate"    "serious"    
    ## [731] "serve"       "service"     "set"         "settle"      "seven"      
    ## [736] "sex"         "shall"       "share"       "she"         "sheet"      
    ## [741] "shoe"        "shoot"       "shop"        "short"       "should"     
    ## [746] "show"        "shut"        "sick"        "side"        "sign"       
    ## [751] "similar"     "simple"      "since"       "sing"        "single"     
    ## [756] "sir"         "sister"      "sit"         "site"        "situate"    
    ## [761] "six"         "size"        "sleep"       "slight"      "slow"       
    ## [766] "small"       "smoke"       "so"          "social"      "society"    
    ## [771] "some"        "son"         "soon"        "sorry"       "sort"       
    ## [776] "sound"       "south"       "space"       "speak"       "special"    
    ## [781] "specific"    "speed"       "spell"       "spend"       "square"     
    ## [786] "staff"       "stage"       "stairs"      "stand"       "standard"   
    ## [791] "start"       "state"       "station"     "stay"        "step"       
    ## [796] "stick"       "still"       "stop"        "story"       "straight"   
    ## [801] "strategy"    "street"      "strike"      "strong"      "structure"  
    ## [806] "student"     "study"       "stuff"       "stupid"      "subject"    
    ## [811] "succeed"     "such"        "sudden"      "suggest"     "suit"       
    ## [816] "summer"      "sun"         "sunday"      "supply"      "support"    
    ## [821] "suppose"     "sure"        "surprise"    "switch"      "system"     
    ## [826] "table"       "take"        "talk"        "tape"        "tax"        
    ## [831] "tea"         "teach"       "team"        "telephone"   "television" 
    ## [836] "tell"        "ten"         "tend"        "term"        "terrible"   
    ## [841] "test"        "than"        "thank"       "the"         "then"       
    ## [846] "there"       "therefore"   "they"        "thing"       "think"      
    ## [851] "thirteen"    "thirty"      "this"        "thou"        "though"     
    ## [856] "thousand"    "three"       "through"     "throw"       "thursday"   
    ## [861] "time"        "to"          "today"       "together"    "tomorrow"   
    ## [866] "tonight"     "too"         "top"         "total"       "touch"      
    ## [871] "toward"      "town"        "trade"       "traffic"     "train"      
    ## [876] "transport"   "travel"      "treat"       "tree"        "trouble"    
    ## [881] "true"        "trust"       "try"         "tuesday"     "turn"       
    ## [886] "twelve"      "twenty"      "two"         "type"        "under"      
    ## [891] "understand"  "union"       "unit"        "unite"       "university" 
    ## [896] "unless"      "until"       "up"          "upon"        "use"        
    ## [901] "usual"       "value"       "various"     "very"        "video"      
    ## [906] "village"     "visit"       "vote"        "wage"        "wait"       
    ## [911] "walk"        "wall"        "want"        "war"         "warm"       
    ## [916] "wash"        "waste"       "watch"       "water"       "way"        
    ## [921] "we"          "wear"        "wednesday"   "wee"         "week"       
    ## [926] "weigh"       "welcome"     "well"        "west"        "what"       
    ## [931] "when"        "where"       "whether"     "which"       "while"      
    ## [936] "white"       "who"         "whole"       "why"         "wide"       
    ## [941] "wife"        "will"        "win"         "wind"        "window"     
    ## [946] "wish"        "with"        "within"      "without"     "woman"      
    ## [951] "wonder"      "wood"        "word"        "work"        "world"      
    ## [956] "worry"       "worse"       "worth"       "would"       "write"      
    ## [961] "wrong"       "year"        "yes"         "yesterday"   "yet"        
    ## [966] "you"         "young"

``` r
# Begin with at least two vowels and end with at least two consonants
words[str_detect(words,"^[aeiou]{2,}.*[^aeiou]{2,}$")]
```

    ## [1] "authority" "each"      "early"     "east"      "easy"      "eight"    
    ## [7] "ought"

``` r
# Contain a repeated pair of letters (e.g. "church" contains "ch" twice)
words[str_detect(words,"([^ ]{2,}).*\\1")]
```

    ##  [1] "appropriate" "church"      "condition"   "decide"      "environment"
    ##  [6] "london"      "paragraph"   "particular"  "photograph"  "prepare"    
    ## [11] "pressure"    "remember"    "represent"   "require"     "sense"      
    ## [16] "therefore"   "understand"  "whether"

``` r
# Contain one letter other than e that is repeated in at least three places (e.g. “appropriate” contains three “p”s.)
words[str_detect(words,"([^e]{1}).*\\1.*\\1.*")]
```

    ## [1] "appropriate" "available"   "business"    "discuss"     "environment"
    ## [6] "individual"  "paragraph"   "tomorrow"

##### Question 5.

Using the sentences provided in stringr::sentences, find all words that
come after a “number” like “one”, “two”, … “twelve”. Pull out both the
number and the word.

``` r
numbers <-  c("one","two","three","four","five","six","seven","eight","nine","ten","eleven","twelve")
numbers_match <- str_c("(\\b", numbers, "\\b)( \\w+)", collapse= "|")
matches <- str_subset(sentences,numbers_match)
str_extract_all(matches,numbers_match,simplify=TRUE)
```

    ##       [,1]           
    ##  [1,] "seven books"  
    ##  [2,] "two met"      
    ##  [3,] "two factors"  
    ##  [4,] "three lists"  
    ##  [5,] "seven is"     
    ##  [6,] "two when"     
    ##  [7,] "ten inches"   
    ##  [8,] "one war"      
    ##  [9,] "one button"   
    ## [10,] "six minutes"  
    ## [11,] "ten years"    
    ## [12,] "two shares"   
    ## [13,] "two distinct" 
    ## [14,] "five cents"   
    ## [15,] "two pins"     
    ## [16,] "five robins"  
    ## [17,] "four kinds"   
    ## [18,] "three story"  
    ## [19,] "three inches" 
    ## [20,] "six comes"    
    ## [21,] "three batches"
    ## [22,] "two leaves"

##### Question 6.

Using the sentences provided in stringr::sentences, view all sentences
that contain the word “good” or the word “bad”. Get the sentence numbers
where those words occur. Use str_replace_all() to replace the word “bad”
with the word “horrible” and the word “good” with the word “great”. Look
at the sentence numbers you found before to verify the words were
replaced correctly.

``` r
matches <- str_detect(sentences,"good|bad")
index <- which(matches)
match_sentences <- str_subset(sentences,"good|bad")
sentences_modif <- str_replace_all(sentences, c("good"="great", "bad"="horrible"))
sentences[index]
```

    ##  [1] "The wrist was badly strained and hung limp."       
    ##  [2] "We frown when events take a bad turn."             
    ##  [3] "We admire and love a good cook."                   
    ##  [4] "Sell your gift to a buyer at a good gain."         
    ##  [5] "These pills do less good than others."             
    ##  [6] "It takes a good trap to capture a bear."           
    ##  [7] "Much of the story makes good sense."               
    ##  [8] "The price is fair for a good antique clock."       
    ##  [9] "The water in this well is a source of good health."
    ## [10] "The team with the best timing looks good."         
    ## [11] "To send it. now in large amounts is bad."          
    ## [12] "The good book informs of what we ought to know."   
    ## [13] "It was a bad error on the part of the new judge."

``` r
sentences_modif[index]
```

    ##  [1] "The wrist was horriblely strained and hung limp."     
    ##  [2] "We frown when events take a horrible turn."           
    ##  [3] "We admire and love a great cook."                     
    ##  [4] "Sell your gift to a buyer at a great gain."           
    ##  [5] "These pills do less great than others."               
    ##  [6] "It takes a great trap to capture a bear."             
    ##  [7] "Much of the story makes great sense."                 
    ##  [8] "The price is fair for a great antique clock."         
    ##  [9] "The water in this well is a source of great health."  
    ## [10] "The team with the best timing looks great."           
    ## [11] "To send it. now in large amounts is horrible."        
    ## [12] "The great book informs of what we ought to know."     
    ## [13] "It was a horrible error on the part of the new judge."
