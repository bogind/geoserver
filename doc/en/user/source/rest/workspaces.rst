.. _rest_workspaces:

Workspaces
==========

The REST API allows you to create and manage workspaces in GeoServer.

.. note:: Read the :api:`API reference for /workspaces <workspaces.yaml>`.

Adding a new workspace
----------------------

**Creates a new workspace named "acme" with a POST request**

*Request*

.. admonition:: curl

   ::

       curl -v -u admin:geoserver -XPOST -H "Content-type: text/xml" 
         -d "<workspace><name>acme</name></workspace>" 
         http://localhost:8080/geoserver/rest/workspaces

.. admonition:: python

   ::
      
      import json
      from requests import request
      from requests.auth import HTTPBasicAuth

      url = "http://localhost:8080/geoserver/rest/workspaces"
      user = "admin"
      password = "geoserver"
      payload = {"workspace":{"name": "acme"}}
      headers = { "Content-Type": "application/json"}

      response = request("POST", url, auth=HTTPBasicAuth(user,password), headers=headers, data=json.dumps(payload))
      print(response)

.. note:: The **Python** example uses a JSON Content-Type

.. admonition:: java

   TBD


*Response*

::

   201 Created

.. note:: The ``Location`` response header specifies the location (URI) of the newly created workspace.

Listing workspace details
-------------------------

**Retrieve information about a specific workspace**

*Request*

.. admonition:: curl

   ::

       curl -v -u admin:geoserver -XGET -H "Accept: text/xml" 
         http://localhost:8080/geoserver/rest/workspaces/acme

.. note:: The ``Accept`` header is optional. 

.. admonition:: python

   ::

      from requests import request
      from requests.auth import HTTPBasicAuth

      url = "http://localhost:8080/geoserver/rest/workspaces/acme"
      user = "admin"
      password = "geoserver"
      headers = {
         "Content-Type": "application/json",
         "Accept": "text/xml"
      }

      response = request("GET", url, auth=HTTPBasicAuth(user,password), headers=headers)
      print(response.json())

.. admonition:: java

   TBD

*Response*

.. code-block:: xml

   <workspace>
     <name>acme</name>
     <dataStores>
       <atom:link xmlns:atom="http://www.w3.org/2005/Atom" rel="alternate" 
        href="http://localhost:8080/geoserver/rest/workspaces/acme/datastores.xml" 
        type="application/xml"/>
     </dataStores>
     <coverageStores>
       <atom:link xmlns:atom="http://www.w3.org/2005/Atom" rel="alternate" 
        href="http://localhost:8080/geoserver/rest/workspaces/acme/coveragestores.xml" 
        type="application/xml"/>
     </coverageStores>
     <wmsStores>
       <atom:link xmlns:atom="http://www.w3.org/2005/Atom" rel="alternate" 
        href="http://localhost:8080/geoserver/rest/workspaces/acme/wmsstores.xml" 
        type="application/xml"/>
     </wmsStores>
   </workspace>

This shows that the workspace can contain "``dataStores``" (for :ref:`vector data <data_vector>`), "``coverageStores``" (for :ref:`raster data <data_raster>`), and "``wmsStores``" (for :ref:`cascaded WMS servers <data_external_wms>`).










