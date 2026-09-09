# thirukkural

The Tirukkuṛaḷ (திருக்குறள்) is a classic work of Tamil Sangam literature consisting of 1330 couplets, or kurals, authored by Thiruvalluvar. This repo provides the Thirukkural as JSON.

**🔍 Search all 1330 kurals → [tk120404.github.io/thirukkural](https://tk120404.github.io/thirukkural/)**

Search runs entirely in the browser over the JSON files in this repo — in Tamil or English, across the couplets, translations, transliterations, and all three commentaries. Filter by பால் or அதிகாரம், and link straight to any kural with `#kural-1330`.

## thirukkural.json

All **1330 kurals**, numbered contiguously from 1 to 1330, under the `kural` key. Every record has all eleven fields populated — there are no gaps.

```json
{
  "Number": 1,
  "Line1": "அகர முதல எழுத்தெல்லாம் ஆதி",
  "Line2": "பகவன் முதற்றே உலகு.",
  "Translation": "'A' leads letters; the Ancient Lord Leads and lords the entire world",
  "mv": "எழுத்துக்கள் எல்லாம் அகரத்தை அடிப்படையாக கொண்டிருக்கின்றன. அதுபோல உலகம் கடவுளை அடிப்படையாக கொண்டிருக்கிறது.",
  "sp": "எழுத்துக்கள் எல்லாம் அகரத்தில் தொடங்குகின்றன; (அது போல) உலகம் கடவுளில் தொடங்குகிறது.",
  "mk": "அகரம் எழுத்துக்களுக்கு முதன்மை; ஆதிபகவன், உலகில் வாழும் உயிர்களுக்கு முதன்மை",
  "explanation": "As the letter A is the first of all letters, so the eternal God is first in the world",
  "couplet": "A, as its first of letters, every speech maintains; The \"Primal Deity\" is first through all the world's domains",
  "transliteration1": "Akara Mudhala Ezhuththellaam Aadhi",
  "transliteration2": "Pakavan Mudhatre Ulaku"
}
```

| Field | Description |
| --- | --- |
| `Number` | Kural number, 1–1330 |
| `Line1`, `Line2` | The two lines of the kural in Tamil |
| `Translation` | English translation |
| `mv` | உரை — டாக்டர் மு. வரதராசனார் |
| `sp` | உரை — சாலமன் பாப்பையா |
| `mk` | உரை — மு. கருணாநிதி |
| `explanation` | English prose explanation |
| `couplet` | English verse couplet |
| `transliteration1`, `transliteration2` | Romanized transliteration of `Line1` and `Line2` |

## detail.json

The structural hierarchy of the work — பால் → இயல் → அதிகாரம் — nested three levels deep:

```
section (பால் / Paal)          3 entries: அறத்துப்பால், பொருட்பால், காமத்துப்பால்
└── chapterGroup (இயல் / Iyal)
    └── chapters (அதிகாரம் / Adhigaram)
```

Each chapter carries `start` and `end`, the inclusive range of `Number` values in `thirukkural.json` that belong to it, so the two files join on kural number:

```json
{ "name": "கடவுள் வாழ்த்து", "translation": "The Praise of God",
  "transliteration": "Katavul Vaazhththu", "number": 1, "start": 1, "end": 10 }
```

Every level has `name`, `transliteration`, `translation`, and `number`.

## Text normalization

Both files are normalized so that exact-match search, deduplication, and string comparison behave predictably for consumers:

* All Tamil text is **Unicode NFC** normalized. Without this, visually identical strings compare unequal depending on how the consumer's input is normalized.
* Whitespace is single-spaced and trimmed — no leading, trailing, or repeated spaces.
* Where the source text joined two verse lines, they are separated by a single space.

## Running the site locally

`index.html` fetches the JSON files, and browsers block `fetch` over `file://`, so serve the directory rather than opening the file directly:

```
python3 -m http.server
```

Then open <http://localhost:8000>. There is no build step and no dependencies.

## Contributing

Pull requests are welcome — for corrections, additional narratives, or other details. Please keep the conventions above intact: NFC-normalized text, single spaces, and all 1330 numbers present.

## References

* http://www.thirukkural.com/
* http://www.gokulnath.com/thirukurals
