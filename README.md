# Open-CMSIS-Pack-Taxonomy

Open-CMSIS-Pack enables software re-use across software vendors and companies. This repository organizes the usage of `Cclass` and `Cgroup` definitions that provide access to:

- Software components that are defined with the element [`<components>`](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/pdsc_components_pg.html).
- Application Programming Interfaces (API) are defined with the element [`<apis>`](https://open-cmsis-pack.github.io/Open-CMSIS-Pack-Spec/main/html/pdsc_apis_pg.html).

The `Cclass` and `Cgroup` names are used to select software components. The file [`Open-CMSIS-Pack-Taxonomy.yaml`](https://github.com/Open-CMSIS-Pack/Open-CMSIS-Pack-Taxonomy/blob/main/Open-CMSIS-Pack-Taxonomy.yaml) contains the registered `Cclass` names and describes their usage.

Each new `Cclass` name should be registered with an **Mode** (explained below) to avoid conflicts with other software packs.  A `CGroup` name needs to be registered only when there is strict control about the usage.

[**Request a new Cclass name >**](./issues/new?assignees=&labels=new+icon&template=cclass_request.yml)

The following **Mode** types allows validation tools to perform checks:

- **Mode: Open** is used to allow extensions provided by multiple vendors. Every vendor can add additional Cgroup names. As a component has also a Cvendor, an name clash between different vendors can be resolved. Still it is recommended to avoid name clashes at the Cgroup level.
- **Mode: Device** is used to define device specific software components. New Cgroup names are allowed, but each component must have a dependency to a device (otherwise similar to Mode: Open).
- **Mode: Board** is used to define board specific software components. New Cgroup names are allowed, but each component must have a dependency to a board (otherwise similar to Mode: Open).
- **Mode: Controlled** is used to describe that extensions to the Cclass are possible, but controlled by the Open-CMSIS-Pack working group or by the Owner (=vendor). CMSIS, LVGL, or Memfault could be examples for such a Cclass.
- **Mode: Bundle** is used to publish a complete software stack with fixed functionality (i.e. File System, TCP/IP stack, etc.). Additional Cgroup names can only be added using the same Cvendor name. It is possible to have multiple bundles that use the same Cclass name.
- **Mode: API** is used to publish unified API header files. Implementations can be provided by various vendors using a Csub name in the element. Depending on the attribute exclusive one or more implementations may be provided. This mode is triggered by the element <apis> of a software pack.

The implications of the different modes are:
- **Mode: Open** new Cgroup names are accepted. There might be a check for duplicates in other packs.
- **Mode: Device** new Cgroup names are accepted. There is a check for a device condition as the components are device specific.
- **Mode: Board** new Cgroup names are accepted. There is a check for a board condition as the components are boards specific.
- **Mode: Controlled** Cgroup are checked against Open-CMSIS-Pack-Taxonomy.XML. If not present, rejected.
- **Mode: Bundle** new Cgroup names are accepted. There is a check that a bundle with name is defined.
- **Mode: API** same as Mode:Controlled as new APIs can only be added by the Open-CMSIS-Pack working group or by the Owner (=vendor).

> **Note:**
>
> A `Cclass` name that is incorrectly applied may result to unexpected behaviour of the Open-CMSIS-Pack system. Sometimes even established software packs become unusable or users get confused by way components are represented. It is therefore mandantory to register the `Cclass` taxonomy using this repository.
