SEN - Chapter outline

(this rough cut focusses on the "meat", exact references, illustrations and more details about the prototype with screenshots with be added later)

# Motivation and Vision Statement

Although the idea behind personal knowledge graphs dates back to the 1960s with the now famous Zettelkasten method by Luhmann [xx](yy), it only became popular in recent years with the introduction of connected note taking tools like Evernote, Notion, Roam or Obdisian, to name only a few.

On the other hand, there is raising criticism in the usefulness of this approach [xxx](yy), as a graph does not make one any wiser per se, and connections alone do not bring much new insights beyond the fact that the linked information is connected somehow. Without an additional classification on how and why some bits of information are connected, users cannot gather meaningful output, as they cannot navigate and query based on the depth of knowledge they gathered, confined to see only on shallow connections on the surface.

Also, not everything can or should be captured in note taking applications and handled via cloud services, as sophisticated as they may have become.
A lot of valuable information is still locally stored on personal desktop systems in the form of carefully selected documents, ebooks, papers or other media, possibly restricted or private sources, and personal artifacts like project notes, ideas, conecpts, or drafts.

Peronal knowedge graphs should also cover all kinds of information, not only document or media entities, but also various communication (mails), contacts and events (conferences, meetings, etc.) already present in the user's environment, and highly connected to personal data and work that derives from it.

A truly personal knowedge graph needs to live "on the edge", i.e. the user's system, it needs to embrace that existing information, understand its connections, make them visible to the user and allow to navigate and query it.

## A Vision for a Personal Knowledge Graph based on the Semantic Desktop

-- Wise up your Workspace - Why a Personal Knowledge Graph should live in your File System

The most natural and feasible way to implement such a system would be to utilize a modern OS that provides a semantic filesystem, with attributes and relations built-in.

Although many modern filesystems now support custom attributes as key/value pairs, they still don't allow to query for them (there is an experimental patch to make the `find` command support this), and there is no support for relations, reducing their use to static metadata for display in info panels.

Instead of implementing query support and native support for relations beyond simple links directly in the filesystem layer, current semantic desktop solutions introduce a separate data storage like embedded sql databases, adding a lot of overhead and introducing data synchronization issues. They often introduce complex API`s that are more aligned to the semantic web than the desktop, which makes development harder than needed and slows down adoption and user acceptance.

More amibitous efforts in file system development failed because of similar complexity [](WinFS), trying to integrate a full-fledged database into a desktop OS intended for everyday use.

So an ideal solution should be lightweight and integrate transparently and naturally with the desktop the user knows and operates daily, built on a file system that supports semantic queries or can be extended with minimum overhead.

SEN ("Semantic ExteNsions") follows this approach by utilizing and extending the rich infrastucture and API already provided by Haiku, the most prominent open-source descendant of BeOS [](). Files naturally represent entities, as the type system is based on MIME types, properties of entities are stored in custom filesystem attributes, only relations have been ommitted because the original creators of BeOS identified the same fallacies outlined above (the first version of the OS still had a Table and Relations API though).

SEN circumvents this by also storing relations in file system attributes, similar to properties, and providing a very thin API to bridge this extension of the base OS.
For performance, any file that is part of a relation gets a unique and stable identifier (an object id), and relations reference this ID in a single custom attribute. Because both the file ID of the source and the relation IDs pointing to target files are stored in an indexed attribute, they can be queried very efficiently.
Relation properties are stored in additional attributes that need not be indexed, as they are retrieved on demand in near real time.

## How to Build it: The Pillars of the Proposed Solution

* Learning from the Past: A short history of the Semantic Desktop
    * The Role of Metadata in Filesystem Design - From Acorn to UNIX
    * Promising Concepts: Nepomuk and Baloo
    * Problems with Current Solutions
        * Falling into the Complexity Trap
            * Applying Semantic Web Standards to the Desktop
            many projects failed because they tried to build the entire complexity of the semantic web for personal knowledgge graphs, which is not really feasible or sustainable, see e.g. https://www.gnu.org/software/gnowsys/
            * Leaky Abstractions: Missing Usability
        * Neglecting the Performance Impact
        * Missing Query Functionality
    * BeOS - The First Entity-Based Desktop
        * Entities, not Files
        * Universal Interoperability through Custom Attributes
        * Metadata Queries
* Introducing SEN - a modern minimalist user-centric approach
    * Semantic ExteNsions for the Desktop
    * Relations - the missing Link
    * Haiku - the Perfect Prototyping Environment
    * Just Add Magic - SEN API and Platform
    * Desktop Use Cases and Examples
* UNO - a Concept for an Universal NOtebook
    * Simple but Semantic
    * Features and Use Cases
    * Presenting a Prototype
* Outlook, Ongoing and Future Work
    * Integrating Information Extraction and Document Analysis
    * Building Dynamic Relations
    * Rules and Inference of Relations and Attributes
    * Further Desktop Extensions
