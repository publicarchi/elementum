# Julia NLP

Avik Sengupta. Natural Language Processing workshop using Julia, JuliaCon 2018. https://youtu.be/f7RNuOLDyM8

Aussi travail Lindoln sur la collection de corpus langagiers.

0-20’ scraping

22-XX

JuliaCon 2018 | DataDeps.jl and other foundational tools for data driven research | Lyndon White https://youtu.be/kSlQpzccRaI

https://github.com/oxinabox/DataDeps.jl

https://github.com/JuliaText/CorpusLoaders.jl

https://github.com/JuliaText/WordNet.jl

JuliaCon 2018 | Julia as a platform for language development | Jamie Brandon https://youtu.be/BBUrQId0HhQ

https://scattered-thoughts.net

Enhanced String handling in Julia | Scott James. JuliaCon 2018 https://youtu.be/kWqFRGLdqc4

JuliaString.org

https://github.com/JuliaML/MLDatasets.jl/



Glob pour requête un disque dur

```julia
using Glob
```

```julia
files = Glob.glob('data/corpus/pdfs/*.pdf')
```

Plusieurs packages, Taro peut lire n’importe quel format

```julia
using Taro
Taro.init()
```

```julia
meta, txtdata = "Taro.extract(files[1])";
```

```julia
meta
```

information stockée comme un Dict

```julia
txtdata
```

données textuelles

```julia
txtdata = replace(txtdata, '\n', ' ')
```

suppression des espaces, car pas pertinents

```julia
using TextAnalysis
using Languages
```

```julia
getTitle(t) = TextAnalysis.sentence_tokenize(Languages.English(), t)[1];
```

```julia
getTitle(txtdata)
```

Extraire première ligne car le titre

```julia
docs = Any[ ]
for i in 1:1000
  try
    meta.txt = Taro.extract(files[i])
    txt = replace(txt, '\n', ' ')
    title = getTitle(txt)
    dm = TextAnalysis.DocumentMetadata(Languages.English(), title, "", meta["Creation-Date"])
    doc = StringDocument(txt, dm)
    
    push!(docs, doc)
    catch e
	    @show e
  end
end
crps = Corpus(docs)
```

```julia
typeof(crps)
```

