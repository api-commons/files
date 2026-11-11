# Files and Documents

The common file vocabulary -- files and the folders they sit in, the buckets that hold objects, the versions a file keeps and the permissions that share it -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Cloud Storage, Object Storage, Document Management, Documents, File Storage, File Sharing, File Management in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| file | 51 | 44 | id 84%, name 82%, mime_type 66%, created_at 61%, size 61% | files 28, documents 19, assets 7, file 7 |
| folder | 13 | 11 | name 100%, id 91%, parent_id 82%, created_at 64% | folders 11, folder 1, directories 1 |
| bucket | 4 | 4 | name 100% | buckets 4, containers 1 |
| file_version | 3 | 3 | id 100%, name 100% | versions 3 |
| permission | 13 | 13 | id 77%, name 54% | permissions 12, shares 3, share 2, collaborations 1 |

Cohort: 133 providers with harvested OpenAPI, 51 crosswalks. Of the providers exposing a file: 71% create, 78% list, 82% fetch, 49% update, 59% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Once signature documents, database documents and editor documents are set aside, a file agrees on id, name, MIME type, size and created_at -- the shape of a file everywhere. A download URL stays extended: some providers return bytes, some a link.
- Folders agree on their parent (parent_id is core), so a folder tree maps across providers even where files do not.
- Buckets and file versions are thin (4 providers each): most object stores speak the S3 protocol and publish no OpenAPI of their own for it.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The bare Storage tag is not used (energy storage and databases share it); Cloud and Object Storage, Document Management, Documents, File Storage and File Sharing are.
- A document awaiting signature belongs to e-signature: BoldSign, Documenso, DocuSeal, GetAccept, PandaDoc and Nitro are excluded here by name and counted there.
- Database documents (Firestore) and editor documents (Google Docs) are not files.
- OneDrive-style `/drives/{id}/items` and `/folders/{id}/items` count as files; a bare `/items` does not.
- A shared link, a collaboration and a share are one concept, `permission`.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
