***********************
Addon Usage with Python
***********************

There are two ways to access the functionality of the addon with Blender's Python console / text editor (after installation and activation of the addon):

* Import the addon as Python module
* Call the appropriate operator registered in bpy.ops.import_scene 

Option 1: Import the addon as Python module
===========================================

According to the `documentation <https://docs.blender.org/api/blender_python_api_current/info_overview.html#addons>`_: 

        `The only difference between addons and built-in Python modules is that addons must contain a bl_info variable`

Therefore, after installation and activation one can use Python's standard import syntax to import different classes and functions such as: ::

        from photogrammetry_importer.camera import Camera
        from photogrammetry_importer.file_handler.colmap_file_handler import ColmapFileHandler
        from photogrammetry_importer.utility.blender_point_utility import add_points_as_particle_system

The following example shows how to add points contained in a :code:`ply` file as a particle system. ::

        from photogrammetry_importer.file_handlers.point_data_file_handler import PointDataFileHandler
        from photogrammetry_importer.utility.blender_utility import add_collection
        from photogrammetry_importer.utility.blender_point_utility import add_points_as_particle_system

        ifp = r'path\to\Blender-Addon-Photogrammetry-Importer\examples\Example.ply'
        points = PointDataFileHandler.parse_point_data_file(ifp)
        mesh_type = "CUBE"
        point_extent = 0.01
        add_particle_color_emission = True
        reconstruction_collection = add_collection("Reconstruction Collection")
        add_points_as_particle_system(
                points,
                mesh_type,
                point_extent,
                add_particle_color_emission,
                reconstruction_collection
        )


Option 2: Call the appropriate operator registered in bpy.ops.import_scene
==========================================================================

In Blender open the :code:`Python Console` and use :code:`Tabulator` to list the available operators with corresponding parameters, i.e. ::

        >>> bpy.ops.import_scene.<TABULATOR>
        >>> bpy.ops.import_scene.
                                colmap_model(
                                fbx(
                                gltf(
                                meshroom_sfm_json(
                                nvm(
                                obj(
                                open3d_log_json(
                                openmvg_json(
                                ply(
                                x3d(

Or use :code:`Tabulator` with a specific function, e.g. :code:`ply()`, to show the corresponding parameters. ::

        >>> bpy.ops.import_scene.ply(<TABULATOR>
        >>> bpy.ops.import_scene.ply(
        ply()
        bpy.ops.import_scene.ply(import_points=True, draw_points_with_gpu=False, add_points_as_particle_system=True, mesh_type='CUBE', point_extent=0.01, add_particle_color_emission=True, set_particle_color_flag=False, particle_overwrite_color=(0, 1, 0), path_to_transformations="", filepath="", directory="", filter_glob="*.ply")
        Import a PLY file as point cloud


Python Scripting with Blender
=============================

`VS Code <https://code.visualstudio.com>`_ with this `extension <https://marketplace.visualstudio.com/items?itemName=JacquesLucke.blender-development>`_ has many advantages over Blender's built-in text editor. `Here <https://www.youtube.com/watch?v=q06-hER7Y1Q>`_ is an introduction / tutorial video.


