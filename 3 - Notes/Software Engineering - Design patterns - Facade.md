Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Facade is a function that combines multiple other functions / operations. So it hides complexity behind a simple interface.

For example, instead of performing multiple operations one by one:
```python
decoder.decode(file)
encoder.encode(file)
compressor.compress(file)
storage.save(file)
```

We create a facade from it and run one command instead of multiple ones:
```python
class VideoProcessingFacade:
    def convert_video(self, file):
        self.decoder.decode(file)
        self.encoder.encode(file)
        self.compressor.compress(file)
        self.storage.save(file)
        
video_processing = VideoProcessingFacade()
video_processing.convert_video()
```

If a function executes just one simple command, it is not a facade.