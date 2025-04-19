WIP local, not uploaded yet. Actual integration with blender takes longer than it should because blender api is the worst thing ever made
the actual code that needs to be added is essentially as follows. The main holdup is deciding where best to put this
and adding a path storage component to the addon as a whole since it doesnt seem to store import path in a bpy.context variable
pathing is also very inconsisten across games but I will switch to parsing the mesh and mat files (may require json output for mesh) to find the actual paths
```
def apply_texture(obj, texture_path):
  # Create a new material if the object doesn't have one
  for material in obj.data.materials:
      if material.name == "MI_"+basename(texture_path).replace("_D","").replace("T_","").rsplit(".")[0]:
    
              
        # Enable 'Use Nodes'
        material.use_nodes = True
        nodes = material.node_tree.nodes
        
        # Clear default nodes
        for node in nodes:
            nodes.remove(node)
      
        # Create nodes
        bsdf = nodes.new(type='ShaderNodeBsdfPrincipled')
        texture = nodes.new(type='ShaderNodeTexImage')
        try:
            normtexture = nodes.new(type='ShaderNodeTexImage')
            normtexture.image = bpy.data.images.load(str(texture_path).replace("_D","_N"))
            normtexture.image.colorspace_settings.name = 'Non-Color'
        except Exception as e:
            pass
        texture.image = bpy.data.images.load(texture_path)
        texture.image.alpha_mode ='PREMUL'
        output = nodes.new(type='ShaderNodeOutputMaterial')
        # Position nodes
        texture.location = (-300, 0)
        bsdf.location = (0, 0)
        output.location = (300, 0)
      
        # Link nodes
        links = material.node_tree.links
        links.new(texture.outputs['Color'], bsdf.inputs['Base Color'])
        links.new(bsdf.outputs['BSDF'], output.inputs['Surface'])
  ```


<div align="center">

# UEFormat

A model and animation export format created for Unreal Engine game asset extraction. The export format is currently supported by [FModel](https://github.com/4sval/FModel) and [CUE4Parse](https://github.com/FabianFG/CUE4Parse).

</div>

## Supported Plugins
- [Blender](https://github.com/halfuwu/UEFormat/tree/master/Blender)
- [Unreal Engine 5.5+](https://github.com/halfuwu/UEFormat/tree/master/Unreal)

## Blender Features
### Model Data (.uemodel)
- LOD Models (Level of Detail)
- Vertices
- Indices
- Normals
- Texture Coordinates
- Vertex Colors
- Materials
- Weights
- Bones
- Sockets
- Morph Targets
- Collision Geometry (Convex Only)
- Virtual Bones

### Animation Data (.ueanim)
- Location Keys
- Rotation Keys
- Scale Keys

## Unreal Features
### Model Data (.uemodel)
- LOD Models (Level of Detail)
- Vertices
- Indices
- Normals
- Texture Coordinates
- Vertex Colors
- Materials
- Weights
- Bones
- Sockets
- Morph Targets

### Animation Data (.ueanim)
- Location Keys
- Rotation Keys
- Scale Keys
- Float Curves
