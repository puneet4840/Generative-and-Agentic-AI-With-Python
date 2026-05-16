# Implementing Indexing Phase of RAG

Is slide mein hum RAG ka indexing phase code ke though implement karenge.

Indexing Phase:
- Load the documents.
- Divide the documents in chunks.
- Create the Embedding of chunks.
- Store the Embedding in Vector DB.

Ye Indexing phase ke steps hote hain.

<br>

### Step-1: Implementing Load the Documents step of Indexing Phase

**Installing the necessary Libraries**
```
pip install langchain-community
pip install pypdf
```

**Create a directory structure and files in it**:
```
/Implementing RAG
    |- index.py
    |- Mastering_Azure_Cloud.pdf
```

<br>

```index.py```: This file is loading a pdf file into python program and printing in a page.
```
from pathlib import Path
from langchain_community.document_loaders import PyPDFLoader

pdf_path = Path(__file__).parent / "Mastering_Azure_Cloud.pdf"


# Load the file in python program

loader = PyPDFLoader(file_path=pdf_path)

pages = loader.load() # This load method is loading the pdf into pages. We can print page by page.

print(pages[1])
```
loader pdf ko page by page load karta hai. Hum page number dekar particular page ko print karwa sakte hain.

Output:
```
page_content='Azure Portal
Azure provides 3 administration tools to choose from1. The Azure Portal2. The Azure CLI3. Azure PowerShell
● We canusetheAzure GUIportalwebsite(portal.azure.com)tocreate,configure,andalter our Azure subscription resources.● We canlocate theresourceneededandexecute any changes.We have wizardsandtooltips to guide through various administrative tasks.● Pleasenote that we cannotusetheportalto performrepetitive tasks like creating12VMs etc.● Weneedtouseothertoolstoavoiderrors,anditwillalsobeatime-consumingprocessto do on the portal.
The Azure portal can be divided into 3 sections.
1. Left — A list of resources and services to createand manage your Azure environment.2. Center —Adashboardthatyoucantailortomeetyour(PublicorPrivatedashboards)needs.3. Top —Asearchbartoquicklyfindresourcesandservices,anotificationicon,accessto a web-based command line, and more.
● Let’s try to create a resourceandseehow to usethePortal.Forexample,let us ● ClickontheBurgermenuonthelefttopandselectResourcegroupandclickonit.You will get a new Panel.
--Back to Index-- 2
create a resource group called demystify.' metadata={'producer': 'PyPDF', 'creator': 'PyPDF', 'creationdate': '', 'source': 'C:\\Users\\puneetverma02\\OneDrive - Nagarro\\Desktop\\Puneet_DevOPs\\6 - Generative and Agentic AI with python\\7 - Implementing RAG\\Mastering_Azure_Cloud.pdf', 'total_pages': 104, 'page': 1, 'page_label': '2'}
```

<br>
<br>

### Step-2: Dividing the ducoment in Chunks

To uper wale step se humne document ko page by page python code mein load kiya.

Ab is step mein hum document ko chunks mein divide karenge. Chunk mein divide karne ke liye langchain ki ```langchain-text-splitters``` library ka use kiya jata hai.

**Install Python LangChain Library**:
```
pip install -U langchain-text-splitters
```

Document Split Code:
```
# Split the loaded file into smaller chunks

text_splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=400)

splits = text_splitter.split_documents(document=docs)
```

Complete Code:
```
from pathlib import Path
from langchain_community.document_loaders import PyPDFLoader
from langchain_text_splitter import RecursiveCharacterTextSplitter

pdf_path = Path(__file__).parent / "Mastering_Azure_Cloud.pdf"


# Load the file in python program

loader = PyPDFLoader(file_path=pdf_path)

docs = loader.load()


# Split the loaded file into smaller chunks

text_splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=400)

splits = text_splitter.split_documents(document=docs)
```
